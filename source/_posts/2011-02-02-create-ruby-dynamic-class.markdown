---
layout: post
title: "create ruby dynamic class"
date: 2011-02-02 18:24
comments: true
categories: [ruby, class, dynamic, metaprogramming]
---
```ruby
dynamic_name = "TestEval2"

Object.const_set(dynamic_name, Class.new)
dummy2 = eval("#{dynamic_name}")
puts "dummy2: #{dummy2}"
```

```ruby
dynamic_name = "ClassName"
Object.const_set(dynamic_name, Class.new { def method1() 42 end })
ClassName.new.method1 #=> 42
```

```ruby
class_name = 'foo'.capitalize
klass = Object.const_set(class_name,Class.new)

names = ['instance1', 'instance2'] # Array of instance vars

klass.class_eval do
  attr_accessor *names

  define_method(:initialize) do |*values|
    names.each_with_index do |name,i|
      instance_variable_set("@"+name, values[i])
    end
  end
  # more...
end
```

class_eval and const_set are used. 

```ruby
a_new_class = Class.new(Object) do
  attr_accessor :x

  def initialize(x)
    print #{self.class} initialized with #{x}"
    @x = x
  end
end

SomeModule.const_set("ClassName", a_new_class)

c = ClassName.new(10)
```

without class_eval and const_set
You don't really need to use const_set. The return value of Class.new can be assigned to a constant and the block of Class.new is class_eval.
```ruby
ass Ancestor; end
SomeClass = Class.new(Ancestor) do
  def initialize(var)
     print "#{self.class} initialized with #{var}"
  end
end
=> SomeClass
SomeClass.new("foo")
# SomeClass initialized with foo=> #<SomeClass:0x668b68>
```


The following code uses a class factory to create a new class along with getter and setters for the fields passed into it:
```ruby
class ClassFactory
  def self.create_class(new_class, *fields)
    c = Class.new do
      fields.each do |field|
        define_method field.intern do
          instance_variable_get("@#{field}")
        end
        define_method "#{field}=".intern do |arg|
          instance_variable_set("@#{field}", arg)
        end
      end
    end

    Kernel.const_set new_class, c
  end
end

ClassFactory.create_class "Car", "make", "model", "year"

new_class = Car.new
new_class.make = "Nissan"
puts new_class.make # => "Nissan"
new_class.model = "Maxima"
puts new_class.model # => "Maxima"
new_class.year = "2001"
puts new_class.year # => "2001"
```
In Ruby, classes are simply objects like any other, which are then assigned to a constant.  Hence, to create a new class dynamically we instantiate the class Class with Class.new, and then assign it to a constant via const_set (we invoke it on Kernel so that it is a top-level constant like any other class).  We then add the code that makes up the class in a do-end block.

In that do-end block, for each field we invoke define_method twice, first for the getter method and then the setter method with get_instance_variable and set_instance_variable, respectively.  For each field, we create the instance variables (e.g., for make, we use @make).  Note how we make use of passing the argument in for the setter.

Additionally, if I wanted to make the class a sub-class, I could have used Class.new(parent_class)
