---
layout: post
title: "using screen to keep unix sessions active"
date: 2012-11-24 05:54
comments: true
categories: [unix, screen, nohup]
---


In Unix, what is screen, and how do I use it?

The screen program allows you to use multiple windows (virtual VT100 terminals) in Unix.

Note: UITS does not support screen.

###Features###

1. If your local computer crashes, or you are connected via a modem and lose the connection, the processes or login sessions you establish through screen don't go away. You can resume your screen sessions with the following command:

```sh
  screen -r
```

In some cases you may have to manually "detach" your screen session before resuming it. For more information, see the Knowledge Base document Using screen, why can't I re-attach to my session after a lost connection? 

2. The screen program creates multiple processes instead of multiple Unix login sessions, which means that it is resource-efficient. 

3. You can cut and paste between different screens without using a mouse. Thus, you don't need to be on a computer with a windowing environment such as Mac OS, Mac OS X, Windows, or the X Window System. 

4. It has a block copy feature which is similar to the kill rectangle feature of Emacs. 

5. You can copy and paste more than one page at a time, which you cannot do with some clients. You can scroll up more than one page, depending on how many scrolling lines you have set with the  -h  option. 

6. Using the detach feature, you can save screen processes when logging out and resume where you left off, saving the trouble of restarting them.


###Starting screen###

To start screen, enter the following command:

```sh
  screen
```


###General commands###

Note: Every screen command begins with Ctrl-a .


<table cellpadding="10">
  <tr align="left" valign="top">
    <td align="left">
      <code>Ctrl-a&nbsp;c</code> </td>
    <td align="left">Create new window (shell) </td>
  </tr>
  <tr valign="top">
    <td align="left">
      <code>Ctrl-a&nbsp;k</code> 
     </td>
    <td align="left">Kill the current window
  </td>
  </tr>
  <tr valign="top">
    <td align="left">
      <code>Ctrl-a&nbsp;w</code>
    </td>
    <td align="left">List all windows (the current window is marked with "*")</td>
  </tr>
  <tr valign="top">
    <td align="left">
      <code>Ctrl-a&nbsp;0-9</code>
    </td>
    <td align="left">Go to a window numbered 0-9</td>
  </tr>
  <tr valign="top">
    <td align="left">
      <code>Ctrl-a&nbsp;n</code>
    </td>
    <td align="left">Go to the next window </td>
  </tr>
  <tr valign="top">
    <td align="left">
      <code>Ctrl-a</code>&nbsp;<code>Ctrl-a </code>
    </td>
    <td align="left">Toggle between the current and previous window
    </td>
  </tr>
  <tr valign="top">
  <td align="left">
  <code>Ctrl-a&nbsp;[</code> </td>
  <td align="left">Start copy mode
  </td>
  </tr>
  <tr valign="top">
  <td align="left">
  <code>Ctrl-a&nbsp;]</code> </td>
  <td align="left">Paste copied text
  </td>
  </tr>
  <tr valign="top">
  <td align="left">
  <code>Ctrl-a&nbsp;?</code> </td>
  <td align="left">Help (display a list of commands)
  </td>
  </tr>
  <tr valign="top">
  <td align="left">
  <code>Ctrl-a</code>&nbsp;<code>Ctrl-\</code> </td>
  <td align="left">Quit <code>screen</code>
  </td>
  </tr>
  <tr valign="top">
  <td align="left">
  <code>Ctrl-a&nbsp;D</code> (Shift-d) </td>
  <td align="left">Power detach and logout
  </td>
  </tr>
  <tr valign="top">
  <td align="left">
  <code>Ctrl-a&nbsp;d</code> </td>
  <td align="left">Detach but keep shell window open</td>
  </tr>
</table>

Press the Spacebar or Enter to end a command.

**To copy a block**

To get into copy mode, press Ctrl-a [  .

To move the cursor, press the  h ,  j ,  k , and  l  (the letter l) keys. The  0  (the number 0) or  ^  (the caret) moves to the start of the line and  $  (the dollar sign) moves to the end of the line. Ctrl-b scrolls the cursor back one page and Ctrl-f scrolls forward one page. To set the left and right margins of copy, press  c  and  C  (Shift-c). The Spacebar starts selecting the text and ends selecting the text. To abort copy mode, press Ctrl-g .

**To paste a block**

To paste the copied text to the current window (as many times as you want), press Ctrl-a ] .

**Other commands**

To run a program or execute any Unix command in a new window, at the Unix prompt, enter:

```sh
  screen unixcommand
```

Above, replace unixcommand with the appropriate command name.

To automatically start several windows when you run screen, create a .screenrc file in your home directory and put screen commands in it.

To quit screen (kill all windows in the current session), press Ctrl-a Ctrl-\ .

The man pages for screen are quite readable and make a good tutorial. At the Unix prompt, enter:

```sh
  man screen
```


###[Source Link][http://kb.iu.edu/data/acuy.html]###

###If your unix server does not support [screen](/blog/2012/11/24/using-screen-to-keep-unix-sessions-active). It is always a better to run some commands with [nohup](/blog/2012/11/24/using-nohup-to-prevent-processes-stopping-on-disconnect).###



Any questions on this, please feel free to ask. We're here to help...
