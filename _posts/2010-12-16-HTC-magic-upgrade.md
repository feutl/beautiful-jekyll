---
layout: post
title: HTC Magic upgrade to 2.2.1 A1 Mobilkom / Vodafone
date: 2010-12-16
tags: [english, technology]
published: false
---

After Vodafone UK released the 2.2.1 Update for the HTC Magic 32B everyone is going for it. Thats what I did as well, but a Over The Air (OTA) Update is not getting applied to a phone which is not stock.

[![NTT docomo HT-03A front](https://upload.wikimedia.org/wikipedia/commons/f/f8/NTT_docomo_HT-03A_front.jpg)](https://commons.wikimedia.org/wiki/File:NTT_docomo_HT-03A_front.jpg "By HT-03android.jpg: 自分
derivative work: Ch Th Jo (HT-03android.jpg) [Public domain], via Wikimedia Commons")

Mine was running CM 6.1 with different SPL and Recovery Image - therefore I tried more or less everything to get back to Stock 1.6 Donute Version which was shipped with the HTC Magic with Google!

Thats the way it worked for me and in my opinion the easiest approach for everyone and is not needing a special recovery image! Be aware, the language of the Version will be English, I am working on getting German as well.

If you do have a Engineering SPL installed, you can jump to step 3 immediately.

1. Create a Gold Card that means you need a empty MicroSD Card which you can use to upgrade the standard image
[## HowTo ## http://theunlockr.com/2010/03/10/how-to-create-a-goldcard/](http://theunlockr.com/2010/03/10/how-to-create-a-goldcard/)
2. Copy the original Image with a few hacks for the next steps onto the Gold Card
[## HowTo ## http://forum.xda-developers.com/showthread.php?t=548218](http://forum.xda-developers.com/showthread.php?t=548218)
I used ROM v2.53.707.2 (Engineerings SPL v1.33.2010) and renamed it to sappimg.zip on the Gold Card, booted my phone with the volume down key pressed. Follow the instructions
3. Next step is to upgrade a signed stock version were you can apply the 1.6 upgrade
[## Howto ## http://forum.xda-developers.com/showthread.php?t=807899](http://forum.xda-developers.com/showthread.php?t=807899)
Section: DOWNGRADE TO DONUT OTA: Follow the instructions and you have to use your Gold Card to install the sappimg.nbh - could work with a normal card as well but take the secure approach :)
4. Install the OTA 1.6 update - which is also mentioned in the DOWNGRADE TO DONUT OTA Section and reboot your phone. Do not worry about seeing a HTC myTouch 3G bootscreen, thats fine.
5. Set up your APN - in my case A1 Mobilkom / Vodafone ([APN Overview](http://www.androidonhtc.com/wiki/Carrier_network_settings))
```
Name: A1 Mobilkom Austria
APN: A1.net
username: ppp@A1plus.at
passwort: ppp
MMSC: http://mmsc.A1.net
MMS Proxy: 194.48.124.71
MMS Port: 8001
MCC: 232
MNC: 01
```
6.  After switching on my Data Connection and I went to sleep and over night the update to 2.2.1 got installed :) 

For a manual approach and little more details get this [thread](http://forum.xda-developers.com/showthread.php?t=843274)
Have fun with FroYo on your HTC Magic.