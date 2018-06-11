---
layout: post
title: Add extra storage on the fly with LVM2
date: 2011-08-29
tags: [english, technology]
---

How to add extra storage on the fly using LVM. Here are the steps I used to get my 80GB Maxtor(sda) and 60GB Western Digital(sdb) to work together as one logical unit. I am also using ext3 as my filesystem because it supports on-line resizing.

*   Fresh install of Ubuntu Server 8.10
*   Run updates: sudo aptitude update && sudo aptitude safe-upgrade
*   Reboot because of kernel upgrade
*   Figure out what the extra hard drive is (mine is sdb): sudo fdisk -l
*   Partition the hard drive as Linux LVM: sudo fdisk /dev/sdb
*   Initialize partition for use by LVM (on my system sdb1 is swap): sudo pvcreate /dev/sdb2
*   Display attributes of volume groups to find your group name (mine is ubuntu-server): sudo vgdisplay
*   Add my physical volume to my volume group: sudo vgextend ubuntu-server /dev/sdb2
*   Now extend the logical volume root to include the new physical volume: sudo lvextend -L128G /dev/ubuntu-server/root
*   Lastly, resize the filesystem to include the new free space: sudo resize2fs /dev/ubuntu-server/root

Original article posted by [Useful Ubuntu](http://usefulubuntu.blogspot.com/2009/01/add-extra-storage-on-fly-with-lvm2.html)