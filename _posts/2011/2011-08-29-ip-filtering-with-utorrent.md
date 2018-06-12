---
layout: post
title: IP Filtering with uTorrent
date: 2011-08-29
tags: [english, technology]
---

uTorrent has no easy nor automated way to activate IP filtering based on BlueTacks IP list. Anyway - it is possible following some easy steps.

1.  Download Blocklist Pro Security filtering list (the newest I found) [http://blocklistpro.com/download-center/p2p-ip-filters/](http://blocklistpro.com/download-center/p2p-ip-filters/)
2.  uncompress the file to a folder
3.  rename the file to ipfilter.dat
4.  open the folder %AppData%\uTorrent or Users\username\AppData\Roaming\uTorrent
5.  copy the file ipfilter.dat into the folder
6.  within uTorrent open Options/Preferences/Advanced and search for ipfilter.enable and change it to TRUE
7.  restart uTorrent

The list is getting updated daily - writing a script to do the download and copy job would be easier handling it. To verify that the IP filtering is enabled and working in the Logger tab you should be able to read:

`[2011-08-26 09:49:56] Loaded ipfilter.dat (250632 entries)`

Original Article hosted on [ZeroPaid](http://www.zeropaid.com/news/6443/ip_filtering_with_utorrent/)