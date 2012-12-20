---
layout: post
title: "webkit and rspec without x server"
date: 2011-11-06 07:05
comments: true
categories: [rspec, headless, xserver, capybara-webkit, xvfb]
---

## capybara-webkit

problems running capybara-webkit with the Headless gem, Xvfb and our ci server. We use this setup for automatic integration testing and javascript testing of our Ruby on Rails 3.2 app. During the tests it complains that

> webkit_server: cannot connect to X server
need to rspec to config as:

```ruby
require File.expand_path("../../config/environment", __FILE__)
require 'rspec/rails'
require 'rspec/autorun'
require 'capybara/rspec'
require 'capybara/webkit'
require 'headless'

Capybara.register_driver :webkit do |app|
  Capybara::Driver::Webkit.new(app, :ignore_ssl_errors => true)
end

Capybara.javascript_driver = :webkit

# don't run on the local machine (since we don't have xvfb running locally)
if Rails.env.production?
    headless = Headless.new
    headless.start
end
```
