---
layout: post
title: Cacti - Passwords do not match, please retype.
date: 2009-04-24
tags: [english, technology]
---

With the message `Error: Passwords do not match, please retype.` Cacti tried to make my life horrible today, but not with me. 

If you are running Cacti 0.8.7b (which is the standard version located in the Ubuntu repositories) you will be prompted with this error after editing a host using Firefox 3. The error is based on an auto complete bug within the form. There are two solutions to avoid the problem (which worked for me):

1.  Before saving all the settings you have to delete (if not in use) the value in the password field of the SNMPv3 settings and than switch back to your preferred method of fetching information.
2.  Apply the patch which was provided by [RichardBronosky in the Cacti Forum](http://forums.cacti.net/post-139456.html) solving the problem.

The easiest way to apply this patch is to cd to your cacti directory and: 
1. THIS IS IMPORTANT. Verify the validity of the URI like this: `curl -L http://forums.cacti.net/download.php?id=14681`
2. If it looks like a safe patch, then apply it directly from that URI via curl: `curl -L http://forums.cacti.net/download.php?id=14681|patch -p1 -N`