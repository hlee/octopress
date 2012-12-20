---
layout: post
title: "Mountain Lion and Homebrew"
date: 2012-11-12 20:42
comments: true
categories: [mac, gcc , homebrew , ruby gems]
author: https://gist.github.com/1860902
---
[SOURCE](https://gist.github.com/1860902)

Get Mountain Lion and Homebrew to Be Happy:

1) Install XCode 4.4 into /Applications

Get it from the App Store.

2) Install Command Line Tools

In XCode's Preferences > Downloads you can install command line tools.

3) Let Everyone Know Where XCode Is

```c
sudo xcode-select -switch /Applications/Xcode.app/Contents/Developer
```

4) Install X11

Visit http://xquartz.macosforge.org/trac/wiki and download and install 2.7.2+.

You will need to fix the symlink it makes:

```sh
ln -s /opt/X11 /usr/X11
```

5) Reinstall your brews

```bash
brew list
```

Will tell you what you need to check. Try out everything one by one and when one doesn't work brew remove it and then reinstall it. If the install doesn't work, try brew install it --use-gcc to prevent llvm from getting in the way.
You might need to install libxml2 and link it manually to make sure you don't get the wrong xml2-config if your path:

```bash
brew install libxml2  
brew link libxml2
Run brew doctor and fix anything it tells you.
```

You may also need to symlink gcc for certain ruby gems and other stuff like that:

```bash
sudo ln -s /usr/bin/gcc /usr/bin/gcc-4.2
```

Any questions on this, please feel free to ask. We're here to help...
