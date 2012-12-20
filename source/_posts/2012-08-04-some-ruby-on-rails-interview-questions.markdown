---
layout: post
title: "some ruby on rails interview questions"
date: 2012-08-04 18:22
comments: true
categories: [ruby, rails, 'rails3', questions, interview]
---
**what's N+1 problem, how to solve the problem**
```ruby
clients = Client.limit(10)
 
clients.each do |client|
  puts client.address.postcode
end

clients = Client.includes(:address).limit(10)
 
clients.each do |client|
  puts client.address.postcode
end

```
**what's the different with joins and includes**

**explain eager loading and lazy loading**

**how to get the top 10 average rating product name:**
```ruby
Product: name:string, id:integer,
Review: id:integer, rating:integer, product_id: integer
#solution
select p.name from products as p inner join review as r group by r.prouct_id order avg(r.rating) limit 10
```

**using map and reduce to sum up 5 to 26 which is squareable**

```ruby
module SQ
  def square num
    num.times.each do |i|
      return true if i * i == num
    end
    false
  end
end

5.upto(26).inject(0){|sum,x|sum = sum + x if square(x);sum }
5.upto(26).inject(0){|sum,x|sum = sum + (square(x) ? x : 0 ) }
```

**dynamic load**

```ruby
module A
  def check_credit
    puts "A"
  end
end

module B
  def check_credit
    puts "B"
  end
end

class P
  attr_accessor :type
  def process
    #class_eval
    #self << class
      #include eval(type)
    #end
    type.constantize.check_credit

    check_credit
  end
end
```
