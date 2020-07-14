---
title: "Standardization of Messaging"
date: 2019-08-07T12:34:56-07:00
tags: 
  - Opinion
  - Technology
---
Today, there are many messaging platforms to communicate with people. Depending on the circumstance or the person you are trying to reach, you might use a different platform/app to interact with him/her.

## The messaging app ecosystem we live in
Just looking at my phone, I can identify the following apps for messaging others:

* SMS
* Google Hangouts
* Facebook Messenger
* Telegram
* KakaoTalk
* Slack
* Discord
* Microsoft Teams
* WhatsApp

And this list isn't even exhaustive! For Apple product users, iMessage is another important app to add to the list. Why can't there be one messaging platform to rule them all?

## Standardization! We want standardization!
The initial gut reaction to this fragmented ecosystem is usually *standardization*. It's easy to say that if we had standards on messaging, then everyone could adopt those standards and there would be interoperability between app platforms. This sounds good in theory, but does it work in practice?

{{< figure src="https://imgs.xkcd.com/comics/standards.png" alt="xkcd standards comic" >}}

### Making changes to the standard

Take [IRC](https://en.wikipedia.org/wiki/Internet_Relay_Chat) for example. A lot of people would say that IRC is a success story in standardizing an open chat protocol. There are many different implementations of IRC clients as well as servers. This is great, right? It has stood the test of time and people still use it today. Everything is fine and dandy right? 

Except that anyone who has recently used IRC and compared the feature set to newer messaging platforms can agree that IRC's feature set is quite dated. Why has IRC failed to modernize with the rest of the messaging world to add features like rich media, typing indicators, threading, etc.?

This is one of the problems with standardization. Since it is an open protocol that anyone can use and implement, it becomes difficult to push new features. Doing so would require all client & server implementations to make changes and adopt it. I mean, take a look at the adoption of protocols like TLS 1.3, HTTP 2.0 or even IPv6! Adoption is woefully slow when everyone needs to make changes to use the latest version of the protocol.

For an ecosystem like messaging, apps need to move quickly to provide the best value for their users (since there are so many alternatives). As a result, standardization is usually not very high up on the priority list.

On a side note, there is an effort to modernize the IRC protocol, the [IRCv3 Working Group](https://ircv3.net/). But progress has been slow and people are unfortunately moving on from these older protocols.

## Propietary protocols everywhere!

So what's the other end of the spectrum? Every app basically uses its own propietary protocol and interoperability goes out the window. This sucks for end users that have to download a new app for different use cases, but what benefit do we get?

Because there is no open standard, the authors can change the protocol at any time as long as their app doesn't break. There's much less coordination to go through to push out new changes as long as their app does not break. This allows faster iteration, allows easier experimentation, and pushing out features quickly. As a result, users benefit by getting features which entices them to stay on a given platform.

## Final thoughts

Don't get me wrong, I'm a big fan of open standards and not advocating that everyone invents their own propietary protocol. I just felt like there's always a push to use open standards all the time, without acknowledging the reasons behind wanting to use priopietary protocols under the hood. At the end of the day, each end of the spectrum has it's own pros and cons and deciding which one to use is usually a compromise.
