---
layout: post
title: "Using Deligate in ActiveRecord to avoid dots"
date: 2012-11-14 09:55
comments: true
categories: [rails, activerecord, deligate]
---

##Adding deligate method in the model##

There are various situations where we might be using methods from the child
model from its parents model.

Common example is user and posts

```ruby
class Post
  belongs_to :user
end

class User
  has_many :posts
end
```

To make a call to find a post with category 'ruby' for a User

```ruby
User.first.posts.find_by_category('ruby')
```

If this is being used in multiple places, adding a deligate will make our life easy, thereby avoiding mulitple dots. 
Also User model doesnt have to know the inner methods of the posts model and a logic change in the model Post would not require multiple changes

```ruby
class Post
  belongs_to :user
  delegate :find_by_category, :to => :user, :allow_nil => true
end
```

now the following code will work.
```ruby
User.first.find_by_category('ruby')
```

There is an option to allow prefix as well

Any questions on this, please feel free to ask. We're here to help...
