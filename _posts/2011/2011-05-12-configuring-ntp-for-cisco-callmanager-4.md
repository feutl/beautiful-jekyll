---
layout: post
title: Configuring NTP for Cisco CallManager 4.x
date: 2011-05-12
tags: [english, technology, cisco]
image: /img/2007/cisco.gif
permalink: /configuring-ntp-for-cisco-callmanager-4x/
---

Configuring Ciscos CallManager 4.0 and above to use NTP is not as simple as it should be. First at all, CCM 4.0 is using Windows 2000 as a base system and NTP nor SNTP is enabled there per default. Especially Win2000 is using SNTP, therefore CCM 4.0 is installing a separate NTP service which has to be configured separately.

The NTP configuration file can be found under `C:\WINNT\system32\drivers\etc\ntp.conf` choose your favourite text editor and add your NTP server.

Minutes later our phones and CCM machine should have a synced time and date.

## Resources
* [How To Configure Time Synchronization for Cisco CallManager and Cisco Unity](http://www.cisco.com/en/US/products/sw/voicesw/ps556/products_tech_note09186a008009470f.shtml)