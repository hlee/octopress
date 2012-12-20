---
layout: post
title: "heroku deploy procedure"
date: 2012-12-02 09:09
comments: true
categories: [rails3, heroku, deploy, pg, ssh, git]
---
Just keep record of the procedure to deploy heroku
**install heroku**
heroku gem(deprecated) or [toolbelt](https://toolbelt.heroku.com/)
```ruby
sudo aptitude install heroku-toolbelt
#or for ubuntu
wget -qO- https://toolbelt.heroku.com/install-ubuntu.sh | sh
```
**login with credentials**
```ruby
heroku login
#Enter your Heroku credentials.
#Email: adam@example.com
#Password:
#Could not find an existing public key.
#Would you like to generate one? [Yn]
#Generating new SSH public key.
#Uploading ssh public key /Users/adam/.ssh/id_rsa.pub
```
**create app**
```ruby
heroku create 
heroku rename
heroku help
```
add to git and make a commit 

**push and deploy**
```ruby
#change Gemfile put sqlite3 to development 
#add pg to production
#if you change Gemfile you need to git commit again otherwise heroku will not know
git push heroku master
```
if you got error 

>Permission denied (publickey).
>fatal: The remote end hung up unexpectedly

try
and reference [add keys to heroku](https://devcenter.heroku.com/articles/keys#adding_keys_to_heroku)
```ruby
heroku keys:add ~/.ssh/id_rsa.pub
ssh-keygen -t rsa -f id_rsa
git clone git@heroku.com:stark-dawn-1234.git -o heroku
heroku keys:clear
heroku keys:add
```

**migration and open**

```ruby
heroku run rake db:migrate
heroku run console
heroku logs
heroku open
```

