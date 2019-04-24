---
title: "Migrated to Fastmail"
date: 2017-12-15T12:38:44-08:00
subtitle: "Taking control of your e-mail"
tags:
  - Technology
---
I've recently migrated from using [Mailgun][1] for my domain e-mail to [Fastmail][2].

First of all, before I get into "why Fastmail?", let me explain to you how I've started off using e-mail for my domain.

# Basic catch-all e-mail forwarding
When I originally purchased my domain, I set up my mail so that all e-mail going to `*@jwon.me` (a catch-all e-mail address) would go to my personal Gmail account. Namecheap (my domain registrar), made this extremely simple to do and I was happy with it.

Instructions on how to do that on Namecheap here: https://www.namecheap.com/support/knowledgebase/article.aspx/308/2214/how-to-set-up-free-email-forwarding

# Wanting more granular control
Eventually, however, I wanted to do more complex things. For example, I wanted to turn certain e-mail addresses into mailing lists so that e-mails sent to these mailing lists would go to multiple people (i.e. family members). For example, I wanted to be able to create something like `family[at]jwon[dot]me` to go to 4 different e-mail addresses. 

Namecheap's forwarding service was too simple to do that. so I started to look around.

# Enter Mailgun
I eventually landed on [Mailgun][1], a *free* service that did exactly what i wanted. Also, they were a [API-driven service][3] so possibilities were endless! I was able to create those mailing lists that I was speaking of earlier, and I got all of my e-mail forwarded to my personal Gmail account. 

For several years my MX records were pointed at Mailgun and I was happy. I was receiving e-mail fine and my needs were met.

# About free services
One thing that I've recently been coming to realize about free services is that _if you're not paying for it, you're the product_. Especially for services like Gmail, where they've created a very polished product, I got fed up with the ads and knowing that my data was being used to infer more about who I am. Also, I wanted to try exploring with Desktop clients for e-mail instead of webapps, and knew that using Gmail with IMAP was a hassle due to the way labels were handled.

I started looking for alternatives and I realized that I was probably going to have to go with a paid product.

I narrowed my search down to two services:

**[Fastmail][2] and [Protonmail][4]**

# Protonmail
I was a big fan of Protonmail since day 1. I love the idea of encrypted-at-rest e-mail, meaning that not even Protonmail could read my e-mail. From their perspective, they're storing binary blobs. I liked that they were a privacy-first company and that they offered a VPN service as well (ProtonVPN).

However, there were a couple things that they were lacking that I was looking for:

1. They did not support the "mailing list" type of forwarding that I found to be extremely useful in Mailgun. They did have a catch-all e-mail address and separate identities for multiple sending addresses, but I could not create a mailing list.
2. IMAP support was... indirect. They had [ProtonMail Bridge][5] which basically runs a local IMAP server for you on your machine so that it could decrypt mail from the Protonmail servers. However, this was only a desktop solution and on mobile you were stuck on using their mobile app. Not that big of a deal, but definitely tying yourself into their ecosystem.

That being said, Protonmail is something that I'm definitely going to keep an eye out for and hopefully in the future I could look towards moving my domain mail to them.

# Fastmail
Fastmail advertises themselves as a simple, fast, mail service. E-mail providers today try to do a lot -- even loading the Gmail webapp takes a long time these days. Fastmail's webapp has a minimal interface that forces you to focus on what you came here to do -- process e-mail. 

I am a big fan of [their blog][8] too. They frequently write about security-specific topics from a technical standpoint. I learned a lot just by reading their posts and I could tell that they took e-mail seriously.

Finally, to fulfill my requirement from Mailgun, they support [Aliases][6] (similar to mailing lists) and [catch-all addresses][7]!

Since they had a 30-day trial, I decided to try moving my DNS records to Fastmail. Make sure you make ALL of the DNS records specified in their setup guide. All of the MX records, SRV records, CNAME records. I missed a couple and my mailing lists did not work until I made all of the appropriate DNS changes. 

After that, all of my e-mail started flowing into Fastmail! They have their own native e-mail mobile app as well, which also works well.

I'm about a week into using Fastmail right now and I have no complaints so far. I want to move most of my e-mail from Gmail to Fastmail. I _want_ to kill my Gmail account but I know that I'll never be able to truly kill it. I'm too invested in the Google ecosystem (with my Pixel phone) and I use the Google Apps suite (Docs, Sheets, Slides)  a lot too. But baby steps is what I'm striving for and I feel like I'm making steps in the right direction.

# Next steps
I want to try looking at Desktop E-mail clients next as well as IMAP mobile clients. I know I can use the webapp, but I think there is a lot to be gained from dedicated apps, and I want to look into what it can provide. :)



[1]: https://www.mailgun.com/
[2]: https://www.fastmail.com/
[3]: https://documentation.mailgun.com/en/latest/quickstart-receiving.html#examples-of-filter-expressions-for-routes
[4]: https://protonmail.com/
[5]: https://protonmail.com/bridge/
[6]: https://www.fastmail.com/help/receive/aliases.html
[7]: https://www.fastmail.com/help/receive/alias-catchall.html
[8]: https://blog.fastmail.com/archive/
