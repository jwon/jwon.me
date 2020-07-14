---
title: "Migrated to Hugo"
date: 2017-11-10T23:39:58-08:00
subtitle: "static site generation ftw!"
toc:
  enable: false
tags:
  - Technology
---
As of today, I've officially migrated my blog from Wordpress to [Hugo][1]!

I've always wanted to migrate from using a dynamic application blogging platform to simple markdown files for blogging. As a dynamic app, not only is Wordpress a target for exploits and vulnerabilities, it really is overkill if all you want to do is to post content.

I first read through the [Hugo Documentation][2] to get a understanding of how Hugo works, then I used the [wordpress-to-hugo-exporter][3] to get my data out of Wordpress and then started tinkering around with the structure to get it to work with Hugo.

Some things that I thought were useful to know:

* [Aliases][4] are awesome. They allow you to redirect old URLs to the new directory structure that Hugo likes
* Use a service like [Netlify][5] to make deployments as simple as pushing to a git repo.
* Google Analytics & Disqus integration on Hugo is dead simple. I love how easy they made it to add it to a Hugo site!

Things I need to figure out a better solution for:

* Rich media in posts. Right now I commit the images to git. As convenient it is, I feel like using git as a blob storage is not the way to go...
* Resizing images. This is something a dynamic app like Wordpress did really well. It provided an easy way to upload images, and then it would automatically create several sizes of the image for you. This is now a manual process in Hugo. 

Overall, I like my new setup, and I look forward to writing more as the barrier to entry for writing a post is **much** lower now. 😇 

[1]: https://gohugo.io/
[2]: https://gohugo.io/getting-started/quick-start/
[3]: https://github.com/SchumacherFM/wordpress-to-hugo-exporter
[4]: https://gohugo.io/content-management/urls/#aliases
[5]: https://gohugo.io/hosting-and-deployment/hosting-on-netlify/
