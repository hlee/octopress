---
layout: post
title: "Sudo vs RVMSudo"
date: 2012-12-02 08:42
comments: true
categories: [rvm, sudo, rvmsudo]
---


[RVM](https://rvm.io) is a great command-line tool which allows you to easily install, manage, and work with multiple ruby environments from interpreters to sets of gems. 
This is exactly what makes it special, its easy to [install RVM](https://rvm.io/rvm/install) with just a few commands..

Installing RVM:

```sh
curl -L https://get.rvm.io | bash -s stable
source ~/.bashrc
```

Source is to load bashrc in the same window. 
Now just use

```sh
rvm install 1.9.3
rvm use 1.9.3
```

and it now you can start using ruby version 1.9.3 and switch or add more
versions and install gems in its own version.

In spite of having such features to help the user, everything from there runs only for the logged in user, there may be times where you must run Ruby scripts with RVM as root (or another user) via sudo. 

But if you do this after installing rvm:

```sh
sudo ruby script.rb
```

It would problably not work at all or would be using the system installed
version of ruby(which might be old). Do not forget to check the version of the ruby when you do a
sudo, if it runs!

```sh
sudo ruby -v
```


sudo always starts a new subshell and runs as root from the current user. That new subshell's environment will be completely different, and which means that it does not contain RVM or the other paths. 
There is a workaround, where you can manually add the path by finding them.
Not a great idea, but works.

RVM has a solution for running sudo with the environments, the 'rvmsudo' command. It will pass on any environment variables that RVM set up to get you to the correct Ruby. 
This includes the following variables

- $PATH 
- $GEM_HOME
- $GEM_PATH 
- $BUNDLE_PATH 


So to run the same ruby script script.rb, simply use the Ruby you want and run it with rvmsudo.

```sh
rvm use 1.9.3
rvmsudo ruby script.rb
```
As always, running commands as the root user with elevated privileges, needs to be carefully done since they can alter settings and install unwanted features to all users of the system. 
[Follow our friendly trusted neighborhood spidey.. With Great power comes Great Responsibility]
