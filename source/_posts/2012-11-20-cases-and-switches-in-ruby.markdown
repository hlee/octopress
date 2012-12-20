---
layout: post
title: "cases and switches in ruby"
date: 2012-11-20 13:13
comments: true
categories: [ruby, syntax, switch case, operators]
---

One of the common questions that we get about people coming from other
programing languages is with the way switch cases work in ruby.

The case..switch works like a '===' operator and not like a '==' operator.
Here are a few examples of how it work. Here are a few examples of how it works.

**Syntax:**

```ruby
case value_returning_argument
when case_1
  case_statement_list_1
when case_2
  case_statement_2
else
  case_statement_else
end
```


**Example 1:**

A simple example would be:

```ruby
puts "Enter some value: "
some_value = gets.chomp

case some_string
when 'some', 'other'
  puts 'Entered some other value'
when 'no'
  puts 'Entered no value'
else
  puts 'Why did you enter that value??'
end

```

**Example 2:**

Here's an example that accepts regular expression

```ruby
print "Enter a value: "
some_string = gets.chomp
string_type = case
  when some_value.match(/^\d+$/)
    'Number'
  when some_value.match(/^[a-zA-Z]+$/)
    'String without Numbers'
  else
    'Some text'
  end
```

**Example 3:**

Here's an example that works with a range

```ruby
case some_string
when 1..5
  puts "Between 1 and 5"
when 6..8
  puts "Between 6 and 8"
when 9
  puts "Entered 9"
end
```

**Example 4:**

The parameter for case is optional

```ruby
case
when some_string=='hi'
  puts "you just said hi"
when some_string=='there'
  puts "you just said there"
else
  puts "whatever..!"
end
```


Any questions on this, please feel free to ask. We're here to help...
