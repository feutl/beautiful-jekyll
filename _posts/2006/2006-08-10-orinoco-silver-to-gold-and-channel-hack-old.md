---
layout: post
title: ORiNOCO Silver to Gold and Channel Hack (old version)
date: 2006-08-10
tags: [english, technology]
---

[Link zur original Site](http://www.andrewhakman.dhs.org/orinoco/)

## DISCLAIMER:
> As always, you, and solely you, are responsible for what you do to your hardware, and how you use your hardware. The information provided on this page is strictly for educational purposes. Some things described here may be illegal in certain regions. You may damage your hardware if you don't follow the instructions exactly. Use at your own risk.

## A New Safer and more Universal Way

Will be described here later or go to [Lincomatic's Site](http://www.lincomatic.com/wireless/software.html) and download Alchemy. With your card inthe computer and windows running, run alchemy, select the card from the list, and follow the instructions it gives you. After it's finished, you still need to flash the firmware to plug the new PDA values back into the firmware just like the manual DOS hack.

__This is the OLD Manual Method - Do NOT use this method. For information only__

## Background Information
ORiNOCO cards at first do not seem very similar to PRISM based cards, although at a firmware structure level, they are quite similar. Both have an area in NVRAM called the PDA, or Production Data Area, which holds PDR's, or Production Data Records. PDR's hold key information about each wireless card, such as the MAC address, serial number, available channels, manufacturer id, etc etc. By changing the values of the right PDR's, one can change the MAC address, serial number, available channels, or encryption settings. The changed PDR's will not take effect immediately though. The PDR's are used to plug values into the firmware as it's being written to the flash memory of the card. These same hacks can be applied by directly changing the firmware and then flashing it, but each new version of firmware that comes out would also need to be changed if that method were used. Changing the PDR's permanently changes the card's attributes as the PDR values will be plugged into any firmware flashed onto the card, and thus the card only needs to be 'hacked' once. Now, on to the fun stuff...

## Things you will need
There are a few things you should have handy before you begin:

*   A NEED to perform this hack - if you don't NEED extra channels or 128bit encryption on your 'silver' card, STOP now, this hack is not for you
*   An ORiNOCO card (duh)
*   A blank floppy or a dos partition (true dos, not a dos window)
*   orinocohack.img bootdisk image file (if you're going the disk route) or flash.exe, flashold.exe and flash.ini
*   Winimage or similar to write the image to the disk
*   A PC with floppy drive (or dos partition) and pcmcia controller*
*   A PC with floppy drive (or dos partition) and pcmcia controller*
*   A PC running windows and pcmcia slot to run the ORiNOCO firmware update utility

*If you have trouble reading or writing back the pda, try a different pc with a different pcmcia controller in it. 

## The Procedure
1.  Make your boot floppy using the image above using Winimage (or equivalent). Make sure you're not using a crap floppy (format it first and make sure it has no bad sectors)
2.  Boot your pc off the floppy from power off. Just restarting from windows and booting from the floppy can leave the pcmcia controller in an unknown state. Choose "3\. Clean boot" off the FreeDos menu (no cd-rom is required)
3.  Remove other pcmcia cards and insert your ORiNOCO card
4.  Run "flash -5v -pd orinoco.pda" to dump your card's current pda to orinoco.pda. If you get "Unknown coontroller (or controller not found)", make sure you powered off and on before booting from the floppy as noted above, or try a different pc with a different pcmcia controller.
5.  Use Edit (not notepad) to open orinoco.pda
6.  To change the encryption (silver to gold) and manufacturer to ORiNOCO if you have a branded card:
    1.  Locate the line starting with "6 109"
    2.  Change it so the whole line is "6 109 3 3 2b 0 0" - spacing is IMPORTANT
7.  To get the extra channels (1-14):
    1.  Locate the line starting with "2 104"
    2.  Change it so the whole line is "2 104 3fff" - again, spacing is IMPORTANT
8.  Save the changes and exit Edit
9.  Run "flashold -5v -p orinoco.pda" to flash your new pda to the card. Ignore the "Verify - BAD" error, the error is because the older version of flash.exe that can write the pda, can't read it properly (why flash.exe is used to read the pda, and flashold.exe is used to write it).
10.  Boot into windows
11.  Run any version of the ORiNOCO firmware updater (if you want an older version, check <a>here</a>) (or try Avaya ones if you have problems with the ORiNOCO ones) to flash the firmware, which plugs in your new PDA values

That's it, your card should be upgraded with higher encryption, extra channels, or both depending on which PDR(s) you changed.

This procedure also applies to PRISM based cards to get the extended channels, just don't change the "6 109" line.

It may also be possible to increase the TX power with a PDR. I'm currently looking into this and will update this page when I know more. 

## Acknowledgements from Andrew Hakman
Thank you to "steve!" on the [seattle wireless development](http://www.seattlewireless.net/) mailing list who inspired me to look into this more.

This is directly based off of this [avaya hack](http://thefilevault.org/wardriving/avayahack/) by Rusty Chiles. The main difference between his instructions and these being using 2 different versions of flash.exe to extract and write back the firmware. Also based on [this](http://lists.shmoo.com/pipermail/hostap/2003-July/003558.html) e-mail by Wilfried Klaebe to the hostap mailing list describing changing the firmware directly (rather than the PDA) to get all the channels. I don't get where F3FF comes from (as opposed to 3FFF) - must be an big/little endian thing. I never did try F3FF - it might work as well.

As always, if you have questions or problems, feel free to contact me at [andrew_dot_hakman_at_gmail_dot_com](mailt:andrew_dot_hakman_at_gmail.com)