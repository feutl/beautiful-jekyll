---
layout: post
title: Debug AS number for EIGRP on Cisco Routers
date: 2011-10-28
tags: [english, technology, cisco]
permalink: /debug-as-number-for-eigrp-on-cisco-routers/
---

If you have ever wondered how to find out an AS number of an existing EIGRP process, this is the article answering it. It is simple to get the information if you have access to the router - but what to do if you do not have access and want to join the EIGRP process with a new router.

* First you need a direct connection with the router running the EIGRP process you want to join
* Now we start an EIGRP process on our router (which we can control) and choose a random number for the process. Without that, our routers won't start chatting with each other over EIGRP
* Next step is to create an ACL to filter the packets - this creates less information overhead  `access-list 103 permit eigrp any host 224.0.0.10`
* Using the created ACL we start our debug _debup ip packet 103_
* We do get the IP address of our EIGRP neighbour using the debug. This information is used to create a new ACL Note: that is done to do not overload the router with too much debug information
* our second ACL to get more but filtered information by including the IP from before `access-list 102 permit eigrp host x.x.x.x host 224.0.0.10`
* if everything is set-up properly we can start the next debug without killing our router (otherwise you are going to see a lot of information - which is forcing you to power cycling your router :D ) `debug ip packet 102 dump`

Now we do get something like the sample output below:

```
CoreRouter#debug ip packet 102 dump
IP packet debugging is on (dump) for access list 102
CoreRouter#no debug all
*Mar 8 06:32:11.580: IP: s=150.150.15.15 (FastEthernet0/0.1), d=224.0.0.10, len 60, rcvd 2
07DF1A00: 0100 5E00000A ..^...
07DF1A10: 001BD495 A8E80800 45C0003C 00000000 ..T.(h..E@.&lt;....
07DF1A20: 015832FB 96960F0F E000000A 0205EE36 .X2{....`.....n6
07DF1A30: 00000000 00000000 00000000 00000096 ...............
07DF1A40: 0001000C 01000100 0000000F 00040008 ...............
07DF1A50: 0C040102 ...
```

The line with the leading zeros is the one we need: `07DF1A30: 00000000 00000000 00000000 00000096 ...............`

Take the value after the double point, start your on-board calculator and convert the number from HEX to Decimal and you do have the AS number of your neighbour - in this case it is 150.