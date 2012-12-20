---
layout: post
title: "Using nohup to prevent processes stopping on disconnect"
date: 2012-11-24 05:32
comments: true
categories: [unix, nohup, screen]
---


**nohup** is an unix command which prevents "hangups on logout" which also means that if you decide you need to logoff the from the session with the server, the  command will continue to run as the user.

Syntax:

```sh
nohup run_command &
```

run_command in the above Syntax is the name of the command you want to run.

And the & at the end of the line makes the process run in the background. Once the command starts you can then continue to issue other commands or logout if you choose so. After executing the above command you'll see this displayed on the command line, and you may need to press the <enter> key before being able to enter other commands.

This means that all the output from the command will go into a file called "nohup.out" in the current working directory. You can tail the same to check the logs.

```sh
tail -f nohup.out
```


Also we can alternatively output the text from the command to a different file using redirection.

```sh
nohup run_command > run_command.log &
```


###If your unix server supports [screen](/blog/2012/11/24/using-screen-to-keep-unix-sessions-active). It is always a better option with more features.###


Any questions on this, please feel free to ask. We're here to help...
