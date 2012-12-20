---
layout: post
title: "Setting up a development mailer for Rails with a gmail account"
date: 2012-11-24 06:42
comments: true
categories: [rails, actionmailer, sendmail, gmail]
---

Setting up the rails mailer for development purposes is much easier. using the
action mailer to configure the gmail services, is just a few commands and
configurations away...

Make sure that these settings are not used in production. 

1. Firstly [Sign Up](https://accounts.google.com/SignUp) for a dummy gmail account. 
2. Next add the following configuration in development.rb

File: config/environments/development.rb

```sh
config.action_mailer.raise_delivery_errors = true
config.action_mailer.delivery_method = :smtp
config.action_mailer.smtp_settings = {
  :address              => "smtp.gmail.com",
  :port                 => 587,
  :domain               => '<your_domain>',
  :user_name            => '<user_name>',
  :password             => '<password>',
  :authentication       => 'plain',
  :enable_starttls_auto => true  }
```

Login to the gmail account and check the sent mails, to preview the sent mail.

There's a lot more that can be done with this, check the [Rails Guids](http://guides.rubyonrails.org/action_mailer_basics.html#action-mailer-configuration-for-gmail) for more information.


Any questions on this, please feel free to ask. We're here to help...
