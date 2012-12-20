---
layout: post
title: "Setting up Heroku"
date: 2012-11-15 11:01
comments: true
categories: [deployment, rails] 
---


##Here are the steps to push a rails project to Heroku##

1. Install Heroku


```sh
gem install heroku
```


**2. Create a heroku login with email and password**

```sh
heroku Create
```

3) Change the name of the app

```sh
heroku apps:rename demo-app 
```

[devcenter rename link](https://devcenter.heroku.com/articles/renaming-apps)

4) Push the file to heroku

```sh
git push heroku master
```

[devcenter git link](https://devcenter.heroku.com/articles/git)

5) Check the database

```sh
heroku run rake db:version
```

[devcenter rake link](https://devcenter.heroku.com/articles/rake)

7) Perform a db migrate 

```sh
heroku run rake --trace db:migrate
```

8) Console: 

```sh
heroku run console
```

Further reading:
----------------------

[devcenter link](https://devcenter.heroku.com)

Any questions on this, please feel free to ask. We're here to help...
