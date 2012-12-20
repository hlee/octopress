---
layout: post
title: "Initializing Custom YML Configuration Variables for Different Environments in Rails"
date: 2012-11-26 22:22
comments: true
categories: [rails, yml, configuration, environments]
---

Another common problem that rails developers face while developing web
applications that connect to multiple external systems and api's is configuring
the the same parameters for different environments.

The simplest way - 


- Add a folder to the config folder of your application

- Add all the configuration in as a yml file, like how we use the database.yml
   with all the environments in it

sample file: config/google_api.yml


```yml
development: &default_settings
  google_analytics_id: 'UA-xxxxxxxx-1'
test:
  <<: *default_settings
sandbox:
  google_analytics_id: 'UA-xxxxxxxx-2'
staging:
  google_analytics_id: 'UA-xxxxxxxx-3'
production:
  google_analytics_id: 'UA-xxxxxxxx-4'
```
  the &default_settings and *default_settings can be used to pass the same
  values into another yml

- add the following to your rb file:

  File: config/environment.rb

```ruby
# Load the rails application
require File.expand_path('../application', __FILE__)

# Auto Load APP_CONFIG for the corresponding environment configuration
APP_CONFIG = HashWithIndifferentAccess.new
load_files = Dir["#{Rails.root}/config/app_config/*.yml"].each do |file|
  APP_CONFIG.merge!(YAML.load_file(file)[Rails.env])
end

# Initialize the rails application
Livegamer::Application.initialize!

```

  The above code adds all the yml files inside the folder we created(app_config) under the config folder to a
  hash(APP_CONFIG).

- Now we can use get the google analytics id with the following

```ruby
google_id = APP_CONFIG['google_analytics_id']
```

  This would return the corresponding configuration variable depending upon the
  environment.


  Simple.. :)


  Any questions on this, please feel free to ask. We're here to help...
