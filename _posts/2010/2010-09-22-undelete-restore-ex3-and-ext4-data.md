---
layout: post
title: Undelete / Restore ext3 and ext4 Data
date: 2011-11-12
tags: [english, technology]
---

I stumbled over a very cool tool called extundelete. It promises to let you undelete/restore files you have trashed from your harddisk. I stumbled over it after deleting about 1TB of data on my QNAP Nas and actually it works pretty well and also restores the file names.

Not so amusing was the fact that my QNAP 109II with Q-RAID configured uses an extended ext3 which is not supported by this tool.

Nevertheless [extundelete]("http://extundelete.sourceforge.net/") works well for standard ext3 and ext4 filesystems.