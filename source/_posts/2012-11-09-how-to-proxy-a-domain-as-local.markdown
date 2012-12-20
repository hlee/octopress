---
layout: post
title: "How to proxy a domain to localhost"
date: 2012-11-09 14:29
comments: true
categories: [mac, bash, ipfw]
---
* STEP 1:

Edit your hosts file by typing: 

```bash
sudo vim /etc/hosts
```

Add the following line to the file:

```bash
127.0.0.1 google.com (or whatever other hostname you want proxied)
```


* STEP 2:

Type the following into the command line to (ip foward)set up the server port to 80 in this case it is 3000:
```bash
sudo ipfw add 100 fwd 127.0.0.1,3000 tcp from any to any 80 in
```

Any questions on this, please feel free to ask. We're here to help...
