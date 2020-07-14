---
title: Cyanogenmod 9 on HTC EVO 4G LTE
date: 2012-07-24T17:42:35+00:00
aliases: [/2012/07/24/cyanogenmod-9-on-htc-evo-4g-lte/]
toc:
  enable: false
tags:
  - Technology

---
After using the stock ROM for the past 2 months, I finally decided to try CM9. I originally wanted to wait until a stable release came out for CM9, but the more I used stock, the more I didn't like it.

I'm currently running the 7/5 build of CM9, and I have to say -- I'm loving it. I forgot how great AOSP roms were. ^_^

Couple things though:

1) I took the OTA for my phone when I was on stock, which meant that my HBOOT got updated. Meaning that as of writing, there is no way to attain S-OFF on the bootloader. I'm still able to get root, install a custom recovery, etc. through htcdev unlock, but I'm still S-ON.

2) One of the disadvantages of having S-ON (besides the ugly "TAMPERED" text on your bootloader), is that you can't flash kernels through the recovery. For the majority of the day yesterday, I had trouble flashing CM9 because I thought all I had to do was to flash the rom through the recovery, wipe data, cache, and dalvik cache, and I'm good to go (at least that was the case on my OG EVO). After asking in the #htc-evo-4g-lte irc on freenode, I found out that I had to flash the kernel (boot.img) separately through fastboot. Once I did that, the rom worked!

As I've said before, I'm loving it right now. There's a couple bugs (wifi tethering doesn't work, MMS doesn't work, etc.) but it's good enough for me for daily use. But it looks like CM9 isn't a priority for the devs right now. They're trying to push out CM10 (Jelly Bean) ASAP. I'm pretty excited about that as well. There was a preview the other day, and a lot of people said that it was super smooth and awesome. =) Looking forward to a RC.
