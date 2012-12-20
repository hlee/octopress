---
layout: post
title: "Applying Common Filtering for Rails Api Based Applications"
date: 2012-11-26 22:50
comments: true
categories: [rails, api, configuration]
---

Sometimes there are common sets of fields and id's that we would like the api
to filter before sending the details to the client. It would be great if we can
place them in a common place so that they can be changed anytime.

File: lib/api_config.rb

```ruby
# Filters out the specified list of fields from the API calls
APIFILTERS = ['id','password','secret__internal_id','updated_at','created_at']
```

File: config/initializers/json_config.rb

```ruby
# Requiring the api configuration file
require 'api_config'

class ActiveRecord::Base
  def as_json_with_filter(options=Hash.new)
    options[:except] = APIFILTERS
    as_json_without_filter(options)
  end
  alias_method_chain :as_json, :filter
end

```
the alias_method_chain does two things here:

- firstly it creates an alias method called as_json_without_filter to as_json

- secondly it looks for as_json_with_filter and makes that as the new as_json
  method


The as_json method is one that gets called when the to_json method is called on a
model object or a collection of model objects in rails


example: users controller file

```ruby

class UsersController < ApplicationController

  respond_to :json

  def show
    @user = User.find(params[:id])
    respond_with @user
  end
end

```

the above would call the as_json method of the user model, we have just
overridden the super class to filter out a few fields

```ruby
class User < ActiveRecord::Base

def as_json(options={})
  super(:include => :parents)
end

```


for xml, this is slightly Different

File: config/initializers/xml_config.rb

```ruby
# Requiring the api configuration file
require 'api_config'

class ActiveRecord::Base
  alias_method :to_xml, :old_to_xml
  def to_xml(options=Hash.new)
    options[:except] = APIFILTERS
    old_to_xml(options)
  end
end

```

Any questions, please feel free to ask. We're here to help...
