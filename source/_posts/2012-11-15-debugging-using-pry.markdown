---
layout: post
title: "Debugging using pry"
date: 2012-11-15 22:37
comments: true
categories: [rails, console, pry]
---


**Add the following gems to the Gemfile and bundle install**

File: Gemfile

```ruby
gem 'pry'
gem 'pry-nav'
gem 'pry-remote'
```

**The pry-nav gem allows us to use the following command for adding breakpoints
into our application**

```ruby
binding.pry
```


**Add the following shortcuts to ~/.pryrc to enable navigation while running debugging**

File: ~/.pryrc

```ruby
Pry.commands.alias_command 'c', 'continue'
Pry.commands.alias_command 's', 'step'
Pry.commands.alias_command 'n', 'next'
```

**The pry-remote let us use pry remotely**

Any questions on this, please feel free to ask. We're here to help...
