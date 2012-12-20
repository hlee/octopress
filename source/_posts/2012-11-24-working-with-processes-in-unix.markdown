---
layout: post
title: "Working with Processes in Unix"
date: 2012-11-24 07:08
comments: true
categories: [unix, ps, aux]
---

There are two commands heavily used by developers for checking their pocesses
in unix.

1. Firstly it is the search for processes

```sh
ps -ef | grep search_process
```

or

```sh
ps aux | grep search_process
```

what's the difference, well both do the same task

[link](http://askubuntu.com/questions/129962/ps-ef-vs-ps-aux)

Both list all processes of all users. In that aspect -e and ax are completely equivalent.
Where they differ is output format specifier, -f is "full", while u is "user-oriented". The displayed columns are different:
columns for ps -f
UID PID PPID C STIME TTY TIME CMD

columns for ps u
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND


The difference between ps -ef and ps aux is due to historical divergences between POSIX and BSD systems. 
At the beginning, POSIX accepted the -ef while the BSD accepted only the aux form.

2. Secondly to kill the process that we just found

```sh
kill -9 pid
```

or

```sh
kill -SIGKILL PID
```

or if we know the process name and if the unix system supports

```sh
killall nginx
```

Tip: What if we need to kill all the processes that starts with 'schedule'.
Here it is.. 

```sh
ps aux | grep schedule | grep -v grep | awk '{print $2}' | xargs kill -9
```

A quick description of the steps:

1. "ps aux | grep schedule" searches for the processes by the name schedule and
   returns the rows
2. "grep -v grep" excludes grep from the searched process list (rows)
3. "awk '{print $2}'" prints the second column of all the values returned.
   Which is mostly the process Id, if not choose the corresponding column by
   its number of appearance in the rows returned
4. "xargs kill -9" sends the kill signal to all the selected process Ids

Please make sure that you are searching for the right processes before killing them.


Any questions on this, please feel free to ask. We're here to help...
