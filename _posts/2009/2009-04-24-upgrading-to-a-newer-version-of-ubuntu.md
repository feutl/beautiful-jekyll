---
layout: post
title: Upgrading to a newer Version of Ubuntu
date: 2009-04-24
tags: [english, technology]
---

Based on the fact, that [Ubuntu 9.04](http://www.ubuntu.com/products/whatisubuntu/904features/) was announced today, it is a good idea to explain how to upgrade every Ubuntu Version using the command line.

1.  `sudo apt-get install update-manager-core`
2.  verify `/etc/update-manager/release-upgrades` to use LTS or Normal based on your preferences
3.  `sudo do-release-upgrade`

After that, follow the messages on the screen to upgrade your system to the newest Ubuntu Version.