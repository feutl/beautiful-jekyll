---
layout: post
title: Error opening nvram:/startup-config (Unknown error 0)
date: 2008-10-17
tags: [english, technology, cisco]
permalink: /error-opening-nvramstartup-config-unknown-error-0/
---

`%Error opening nvram:/startup-config (Unknown error 0)`

One of these good morning messages you do not like on a Cisco Router, especially if it is followed by a more cryptic message like `NV: Invalid Pointer values ... `

The solution to fix that problem was a corrupted NVRAM which can be fixed by executing `erase nvram:`

Don't forget to write your running config to your startup - so you have not worry to much about reboots.