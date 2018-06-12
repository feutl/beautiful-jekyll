---
layout: post
title: Most important table to pass CCNA
date: 2008-01-23
tags: [deutsch, technology]
permalink: /most-important-table-to-pass-ccna/
---

msk | mbt | sbn | hst | wmk
----|-----|-----|-----|----
255 | /32 | 0 | - | - 
254 | /31 | 2(128) | 0 | 1
252 | /30 | 4(64) | 2 | 3 
248 | /29 | 8(32) | 6 | 7 
240 | /28 | 16(16) | 14 | 15 
224 | /27 | 32(8) | 30 | 31 
192 | /26 | 64(4) | 62 | 63
128 | /25 | 128(2) | 126 | 127

* msk=last octet of sub.mask ex. 255.255.255.192
* mbt=mask bit sbn=1st subnet address(how many on network)
* hst=number of hosts
* wmk=wildcard mask (last octet) ex. 0.0.0.63

Using binary notation it is easy to wrote this table upside-down.
* sbn = 256 - msk
* number of subnets = 256 / sbn 
* hst = sbn - 2
* Wildcard mask = sbn - 1

Einfach nötig sonst wirds knapp mit der Zeit bei ICND 1 und 2 ;) Gefunden auf [The Legendary 5 Minute Courses](http://www.sadikhov.com/forum/index.php?showtopic=42396)