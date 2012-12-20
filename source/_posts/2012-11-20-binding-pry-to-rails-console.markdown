---
layout: post
title: "binding pry to rails console"
date: 2012-11-20 21:13
comments: true
categories: [pry, rails console, irb]
---

Add the following lines to make the rails console to use pry. make sure that

File: Gemfile

```ruby
gem 'pry'
```

File: config/environments/development.rb

```ruby
silence_warnings do
  require 'pry'
  IRB = Pry
end
```

Any questions on this, please feel free to ask. We're here to help...
