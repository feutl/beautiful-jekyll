---
layout: post
title: Asus Transformer Prime Stuck At Splash Screen
date: 2012-06-28
tags: [english, technology]
---

Rooted my Asus a few days after I have received it. A few month later I unlocked the bootloader and here we go :) Made a backup of the original stock ROM with [TWRP](http://teamw.in/project/twrp2/) and using [Goo.im](http://goo.im/) I updated to latest CyanogenMod. Everything worked fine - until I restored the stock ROM using my backup. 

Recovery worked fine - but after reboot to the new image I was stuck at the ASUS Splash Screen. Fastboot was working but the only options I had was USB or Wipe Data - no Android Symbol there and no Recovery. 

I found this [thread at XDA](http://forum.xda-developers.com/showthread.php?t=1662158) which unbricked my tablet. What you have to do is easy and straight forward, you have to install a new boot.blob - how?

*   you need working ADB, fastboot and a ROM with a proper boot.blob (for example the latest Virtuous Rom)
*   extract the ZIP file and pull the file called 'blob'
*   rename the file as boot.blob and move it to the ADB TOOLS folder and open a Command Prompt
*   boot your Prime into fastboot and select the USB symbol
*   from inside the TOOLS folder type: `fastboot -i 0x0b05 flash boot boot.blob`
*   then type: `fastboot -i 0x0b05 reboot`

This should grant you access to recovery again. From the recovery you are able to use ADB and can push a new ROM to your Prime.

*   open a command prompt and type: `adb push virtuous_prime_s_9.4.2.21_v1.zip /sdcard/`
*   wait until you get a confirmation message (it will look something like 1279 KB/s (334733438 bytes in 255.472s))
*   flash ROM as you would do with any other ROM.

Thanks to the XDA member for solving this.