---
layout: post
title: "Extend vs Include in Ruby Module"
date: 2012-11-24 08:04
comments: true
categories: [ruby, extend, include]
---

**Extend vs. Include**
Modules are used for mixins, ruby's way of handling muliple inheritance without the complications. 
There are two ways to mixin, either include or extend to mix in a module’s functionality into a class. 

**Difference:**


include makes the module’s methods available to the instance of a class,
attached to the instances of the class alone.

```ruby
module Foo
  def foo
    puts 'heyyyyoooo!'
  end
end

class Bar
  include Foo
end

Bar.new.foo # heyyyyoooo!
Bar.foo # NoMethodError: undefined method ‘foo’ for Bar:Class
```

extend makes these methods available to the class as class methods, implemented
with a self \<\< class*

```ruby
class Baz
  extend Foo
end

Baz.foo # heyyyyoooo!
Baz.new.foo # NoMethodError: undefined method ‘foo’ for #\<Baz:0x1e708>

```


More information here at the [source link](http://railstips.org/blog/archives/2009/05/15/include-vs-extend-in-ruby/).

Any questions on this, please feel free to ask. We're here to help...
