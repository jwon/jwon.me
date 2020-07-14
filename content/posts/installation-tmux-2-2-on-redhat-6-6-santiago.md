---
title: Installation tmux 2.2 on Redhat 6.6 (Santiago)
date: 2016-08-17T22:28:48+00:00
aliases: [/2016/08/17/installation-tmux-2-2-on-redhat-6-6-santiago/]
tags:
  - How To

---
Using this guide: <https://www.snip2code.com/Snippet/1232432/Tmux-2-2-is-late-on-redhat>

Make sure that `which tmux` shows that no `tmux` binary is installed before continuing.

## Getting Started

### Install dependencies
```bash
sudo yum install gcc kernel-devel make ncurses-devel
```
### Install latest libevent from source
```bash
$ 
```  

### Install tmux 2.2 from source
```bash
$ cd ~
$ curl -OL https://github.com/tmux/tmux/releases/download/2.2/tmux-2.2.tar.gz
$ tar -xvzf tmux-2.2.tar.gz
$ cd tmux-2.2
$ LDFLAGS="-L/usr/local/lib -Wl,-rpath=/usr/local/lib" ./configure --prefix=/usr/local
$ make
$ sudo make install
```  

## Validating

Close your terminal window.

Open a new shell and check tmux version: `tmux -V`

It should say: `tmux 2.2`
