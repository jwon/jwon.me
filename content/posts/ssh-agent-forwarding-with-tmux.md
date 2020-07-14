---
title: SSH Agent Forwarding with tmux
date: 2016-08-18T20:43:48+00:00
aliases: [/2016/08/18/ssh-agent-forwarding-with-tmux/]
toc:
  enable: false
tags:
  - How To

---
My workstation setup is like this:

  * From my Macbook Pro, I SSH into my Linux Desktop
  * Once I'm SSHed in, I open my tmux sesson. I usually do this with an alias: `alias s='ssh jwon-desktop -t tmux a || tmux new -s main'`

However, I only want to keep my private key on 1 machine (my macbook) and forward the agent to my desktop.

This normally works with SSH forwarding in your `~/.ssh/config` file, but it breaks when you detach/reattach to your tmux session.

The solution to this is outlined here:

<https://gist.github.com/martijnvermaat/8070533#gistcomment-1778689>

In essence, you just need to add to your `~/.bashrc`:
```bash
# Launch SSH agent if not running
if ! ps aux |grep $(whoami) |grep ssh-agent |grep -v grep &gt;/dev/null; then ssh-agent ; fi

# Link the latest ssh-agent socket
ln -sf $(find /tmp -maxdepth 2 -type s -name "agent*" -user $USER -printf '%T@ %p\n' 2&gt;/dev/null |sort -n|tail -1|cut -d' ' -f2) ~/.ssh/ssh_auth_sock

export SSH_AUTH_SOCK=~/.ssh/ssh_auth_sock
```  

And in your `~/.tmux.conf`:
```bash
set -g update-environment -r
setenv -g SSH_AUTH_SOCK $HOME/.ssh/ssh_auth_sock
```  

It's super simple and everything just works. 🙂

Happy tmuxing!
