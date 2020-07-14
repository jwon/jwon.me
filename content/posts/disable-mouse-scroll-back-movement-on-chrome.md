---
title: Disable mouse scroll back movement on Chrome
date: 2017-06-15T16:03:19+00:00
toc:
  enable: false
aliases: [/2017/06/15/disable-mouse-scroll-back-movement-on-chrome/]
tags:
  - How To

---
So, I use the [Logitech Master MX Mouse][1]. One of the things I really like about it is that it has a side-scrolling wheel at the left-side of the mouse:

![][2]

However, the problem with using the side-scrolling wheel and Google Chrome is that whenever I try to scroll left, Google Chrome interprets that as me trying to do the Back movement and go back a page.

However, for OS X, there is a quick fix!

Open up your terminal and run this:
```bash
defaults write com.google.Chrome AppleEnableMouseSwipeNavigateWithScrolls -bool false
```

That should fix your issue!

Happy scrolling. 🙂

 [1]: http://www.logitech.com/en-us/product/mx-master
 [2]: https://assets.logitech.com/assets/64807/mx-master-black-gallery-1.png
