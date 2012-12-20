---
layout: post
title: "RVM Setup and Environments"
date: 2012-11-15 09:23
comments: true
categories: [rvm, ruby, rails]
---

RVM is the Ruby environment manager. Here are some of the commonly used
commands.

**Installing rvm in unix/mac**

```sh
curl -L https://get.rvm.io | bash -s stable 
```

**Setting up the bash profile for enabling rvm**

File: .bash_profile
```sh
[[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm"  # This loads RVM
```

Dont forget to source it, to load the ~/.bash_profile if you're using the same console
```sh
source .bash_profile
```

**Installing new Ruby version**
```sh
rvm install 1.9.3-p327
```

**Listing installed ruby versions**
```sh
rvm list
```


**Updating rvm version from head**
```sh
rvm get head
```


**Setting the default ruby version**
```sh
rvm alias create default 1.9.3
rvm use 1.8.7-p302 --default
```



**For more help use:**

```sh
rvm --help
```


Any questions on this, please feel free to ask. We're here to help...
