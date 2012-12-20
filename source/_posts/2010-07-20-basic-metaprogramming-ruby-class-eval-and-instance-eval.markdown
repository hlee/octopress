---
layout: post
title: "basic metaprogramming ruby class_eval and instance_eval"
date: 2010-07-20 19:21
comments: true
categories: [ruby, metaprogramming, class_eval, instance_eval]
---
```ruby
class A

  def create_method(name)
    self.class.instance_eval do
      define_method(name) { puts "Nice!  I'm #{name}" }
      def human?
        true
      end
    end
  end

  def create_class_method(name)
    self.class.instance_eval do
      self.class.send( :define_method, name) { puts "Nice!  I'm #{name}" }
    end
  end

  def create_instance_method(name)
    (class << self; self; end).class_eval do
      #self.class.send( :define_method, name) { puts "Nice!  I'm #{name}" }
      define_method(name) { puts "Nice!  I'm #{name}" }
    end
  end
```

Sometimes when the book explains a concept or Ruby feature, it sheds light on things I've seen in other people's code – things I've always wondered about. One such example is class_eval and instance_eval. These methods allow you to evaluate arbitrary code in the context of a particular class or object. They're slightly similar to call, apply and bind in JavaScript, in that you are altering the value of self (this in JavaScript) when you use them. Let's take a look at some examples to demonstrate their usage.
```ruby
class Person
end

Person.class_eval do
  def say_hello
   "Hello!"
  end
end

jimmy = Person.new
jimmy.say_hello # "Hello!"
```
In this example, class_eval allows us to define a method within the Person class outside of its original definition and without reopening the class with the standard syntax. This could be useful when the class you want to add this method to is not known until runtime.
```ruby
class Person
end

Person.instance_eval do
  def human?
    true
  end
end
```
Person.human? # true
This example of instance_eval is similar, but evaluates the code in the context of an instance instead of a class. This is confusing at first, because in these examples class_eval creates instance methods and instance_eval creates class methods. There is reason behind the madness, however.

class_eval is a method of the Module class, meaning that the receiver will be a module or a class. The block you pass to class_eval is evaluated in the context of that class. Defining a method with the standard def keyword within a class defines an instance method, and that's exactly what happens here.

instance_eval, on the other hand, is a method of the Object class, meaning that the receiver will be an object. The block you pass to instance_eval is evaluated in the context of that object. That means that Person.instance_eval is evaluated in the context of the Person object. Remember that a class name is simply a constant which points to an instance of the class Class. Because of this fact, defining a method in the context of Class instance referenced by Person creates a class method for Person class.

It may be difficult to wrap your mind around that if you're not familiar with the Ruby object model, but it's still easy to remember how these methods behave with a simple mnemonic device: when called on a class name constant, these two methods will allow you to create methods of the opposite type from their names. MyClass.class_eval will create instance methods and MyClass.instance_eval will create class methods.

If you're interested in metaprogramming or understanding the Ruby object model, I'd definitely recommend the book. It's helped me out tremendously.

I did some experiment with meta programming keywords "class_eval" and "instance_eval'. Sharing some of the examples with you all -


class_eval opens the existing class and adds the methods as defined in an ordinary class, hence they work as instance methods of that class

```ruby
String.class_eval do
  def quack
    p 'quack method'
  end
end

"any string".quack
```

A method defined for class A using class_eval will work as instance method of A
```ruby
class A
end

A.class_eval do
  def some_method
    p 'some_method'
  end
end

A.new.some_method
```
instance_eval on a class will open the class as an instance of class Class. Any method defined will be treated as the method of this instance which is the class. Hence the methods work like class methods
```ruby
class A
end

A.instance_eval do
  def other_method
    p 'other_method'
  end
end

A.other_method
```
instance_eval on an instance of a class will open that instance of the class. Thus it works like a singleton method that is specific to the instance and wont work for other instances of the class
```ruby
class A
end

a = A.new
a.instance_eval do
  def a_method
    p 'a_method'
  end
end

a.a_method  # works for 'a' on which the instance_eval is defined
b = A.new
b.a_method  # doesn't work for 'b'
```
 This is the same as calling instance_eval on the instance 'a' of class A. This again will define a singleton method on the instance
```ruby
class << a
  def show
    p 'this is a method'
  end
end
a  = A.new
a.show
b.show  # doesn't work for 'b'
```
  Can not call 'class_eval' on an instance. class_eval can only be called on classes (which are instances of class Class)
```ruby
class A
end

a.class_eval do
  def show_other
    p 'this is another method'
  end
end

a = A.new 
a.show
b.show
```
