---
layout: post
title: "generate random number in ruby"
date: 2012-11-28 22:27
comments: true
categories: [ruby, random, numbers]
---

Sometimes we would also need to generate x random numbers from n to m

```ruby
x.times.map{n + Random.rand( m - n )}
```

```ruby
Random.new.rand(n...m)
#in ruby 1.9.3
Random.rand(n...m)
```

if you only want to select a random item form array[.](http://stackoverflow.com/questions/198460/how-to-get-a-random-number-in-ruby)

```ruby
%(a b c d e).sample
(n...m).to_a.sample
```
Some other ways by using SecureRandom

```ruby
require 'securerandom'

p SecureRandom.random_number(100) #=> 15
p SecureRandom.random_number(100) #=> 88

p SecureRandom.random_number #=> 0.596506046187744
p SecureRandom.random_number #=> 0.350621695741409

p SecureRandom.hex #=> "eb693ec8252cd630102fd0d0fb7c3485"
```
