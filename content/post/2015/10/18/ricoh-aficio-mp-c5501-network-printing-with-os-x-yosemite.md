---
title: Ricoh Aficio MP C5501 Network Printing with OS X Yosemite
date: 2015-10-18T16:25:45+00:00
aliases: [/2015/10/18/ricoh-aficio-mp-c5501-network-printing-with-os-x-yosemite/]
tags:
  - How To

---
My church has a **Ricoh Aficio MP C5501** printer and I was trying to get network printing working on my Macbook Pro with Yosemite.

The OS X drivers on [Ricoh's Official Website][1] are useless because the printer doesn't come with the PostScript Card...

Therefore, I was left to figure out a custom solution.

Fortunately, our friends at OpenPrinting has provided for us [a PPD file][2] to use. However, it does not work on Yosemite due to sandboxing changes for CUPS.

Anyway, I took the liberty to modify the PPD file with changes to make it work on Yosemite.

Here is the diff of the changes I've made to :
```
44c44
< *NickName: "Ricoh Aficio MP C5501 PXL"
---
> *NickName: "Ricoh Aficio MP C5501 PXL (jwon Modified)"
51c51
< *cupsFilter: "application/vnd.cups-pdf 0 foomatic-rip"
---
> *%cupsFilter: "application/vnd.cups-pdf 0 foomatic-rip"
112c112
< (gs -q -dBATCH -dPARANOIDSAFER -dNOPAUSE -dNOINTERPOLATE %B%A%C %D%E | perl -p -e 's/^\x1b\x25-12345X//' | perl -p -e 's/\xc1\x01\x00\xf8\x31\x44/\x44/g');"
---
> (/usr/local/bin/gs -q -dBATCH -dPARANOIDSAFER -dNOPAUSE -dNOINTERPOLATE %B%A%C %D%E | perl -p -e 's/^\x1b\x25-12345X//' | perl -p -e 's/\xc1\x01\x00\xf8\x31\x44/\x44/g');"
143c143
< *DefaultResolution: 600dpi
---
> *DefaultResolution: 1200dpi
```  

I've also taken the liberty to upload the working PPD file, so you can just download and use it for your own leisure: [Ricoh-Aficio\_MP\_C5501-pxlcolor-Ricoh][3]

Here are the 4 changes that I made:

  * Changed the name of the driver you are using to show that you are using a modified PPD file
  * Commented out the cupsFilter for pdf as without the line, you get the "Filter Failed" error message when you try to print. Source: [link][4]
  * [Applied patch from Matt Broughton][5] to make this PPD file work on Yosemite with stricter sandboxing rules.
  * Changed the default DPI setting from 600dpi to 1200dpi

If you are satisfied with the following changes, check out the PPD file I've uploaded above and try installing it!

# How to install

  1. Download the modified pxlcolor-Ricoh driver: [Ricoh-Aficio\_MP\_C5501-pxlcolor-Ricoh][3]
  2. Install the following two packages from [OpenPrinting][6]: [Foomatic-RIP 4.0.6][7] and [gplgs-8.71.dmg][8]
  3. Add a printer from your System Preferences and use settings like this:
  
    [<img class="aligncenter size-medium wp-image-150" src="https://blog.jwon.me/site/wp-content/uploads/2015/10/Screen-Shot-2015-10-18-at-9.32.57-AM-300x291.png" alt="Screen Shot 2015-10-18 at 9.32.57 AM" width="300" height="291" srcset="https://blog.jwon.me/site/wp-content/uploads/2015/10/Screen-Shot-2015-10-18-at-9.32.57-AM-300x291.png 300w, https://blog.jwon.me/site/wp-content/uploads/2015/10/Screen-Shot-2015-10-18-at-9.32.57-AM-1024x994.png 1024w, https://blog.jwon.me/site/wp-content/uploads/2015/10/Screen-Shot-2015-10-18-at-9.32.57-AM.png 1034w" sizes="(max-width: 300px) 100vw, 300px" />][9](The most important part for this step is that you pick "HP Jetdirect - Socket" as the protocol and for picking the driver under "Use:", make sure you pick "Other..." and manually pick the PPD file that you just downloaded)
  4.  Click "Add" and test the printer!

Hope this helps others that have been struggling with trying to get their Ricoh printer working for for Yosemite!

 [1]: http://support.ricoh.com/bb/html/dr_ut_e/re/model/mpc41/mpc41en.htm
 [2]: http://www.openprinting.org/printer/Ricoh/Ricoh-Aficio_MP_C5501
 [3]: https://blog.jwon.me/site/wp-content/uploads/2015/10/Ricoh-Aficio_MP_C5501-pxlcolor-Ricoh.ppd
 [4]: https://discussions.apple.com/thread/6619722?start=0&tstart=0
 [5]: https://discussions.apple.com/thread/6612623?start=0&tstart=0
 [6]: http://www.linuxfoundation.org/collaborate/workgroups/openprinting/macosxfoomatic
 [7]: http://www.openprinting.org/download/printdriver/macosx/foomatic-rip-4.0.6.230.dmg
 [8]: http://www.openprinting.org/download/printdriver/macosx/gplgs-8.71.dmg 
 [9]: https://blog.jwon.me/site/wp-content/uploads/2015/10/Screen-Shot-2015-10-18-at-9.32.57-AM.png
