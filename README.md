# README

Reworking of Kevin Unkrichs abandoned SaaS theme, dragged kicking and screaming in to Rails 6 & Ruby 3.

With some extra goodies. Uses Boostrap, Devise, Faraday http.

For instructions on how to setup and use the code as a starter project, see installation below. Note that there are some dependencies that may make this project unsuitable for your uses and there are a lot of different ways to go about setting up this project that I will not be covering.

# Installation

Provide code examples and explanations of how to get the project.

After cloning the repository to your computer start by running 'bundle install', 'yarn' and 'rails db:migrate'

rails generate simple_form:install --bootstrap    for simple form
## Setting up Devise & OmniAuth

Devise should work on its own out of the box, but if you would like to use social sign-ups you are going to have to set the environment variables and create apps within the developer sections of Facebook and Google.

First create your applications with Google and Facebook. Links provided below.
- https://developers.facebook.com/apps/
- https://console.developers.google.com/ (Make sure to use/activate Google Contacts and Google Plus)

After creating your applications with the above, set the environment variables to your API keys either remotely or locally.

To do so locally:

Run the below command in the shell:
- source ~/.bashrc

Add these lines to the file:
- export GOOGLE_APP_ID="some_api_key"
- export GOOGLE_APP_SECRET="some_api_key"
- export FB_APP_ID="some_api_key"
- export FB_APP_SECRET="some_api_key"

To do so in Heroku, simply run
heroku set:config environment_variable=value
where 'environment_variable' and 'value' correspond to the local lines.
- For more info, see : https://devcenter.heroku.com/articles/config-vars

Restart your terminal.

Then go into config/initializers/devise.rb and change "your_url.com" to your URL to make the callback URL work.

Add the callback URL in these files to your Google and Facebook applications. Google is somewhat picky about http/https options, so it is safer to add both and configure based on any errors shown.

## Setting Stripe Subscriptions

Similarly to the above, sign up for a Stripe account and retrieve your API keys.

Set the environment variables in the same way as above for the variables 'stripe_publishable_key' and 'stripe_secret_key'.

The test keys are set up to be hard-coded in the application at config/secrets.yml.

By default your Stripe url for webhooks is set to http://your_url.com/stripe/webhooks . I handle webhooks in config/initializers/stripe.rb for the time-being.

Make sure to create plans in the Stripe dashboard and note their id's as you are going to have to pass them to the controller. This is currently handled in the devise/new controller/view. Set your plan name/s in the app/controller/application_controller.rb to direct the user to subscription or not based on whether the plan is free.

## Using Cloudflare and Heroku for free SSL
See the link here to learn how to setup SSL on your site for free:
- https://support.cloudflare.com/hc/en-us/articles/205893698-Configure-CloudFlare-and-Heroku-over-HTTPS


# License

This starter project simply combines existing technologies such as Twitter Bootstrap, Ruby on Rails, Devise & OmniAuth gems, Stripe, and more.

As a result, it is intended to be used simply as a starter template for SaaS projects using Rails and is licensed under the MIT license.



This project uses Ruby 2.3.0 with Rails 5.0


