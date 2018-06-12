---
layout: post
title: Multiple SSH Connections to NetApp Filer
date: 2012-06-28
tags: [english, technology]
---

More often then expected - it is necessary to connect to the Filer using SSH or Telnet. Console access using a serial cable is not always an option - nevertheless the NetApp is supporting those interactive session - but with some limitations.

*   1 Console Session using Serial Port
*   1 SSH/Telnet Session which is interactive and "talks" to you ;) `ssh [-1|-2] [-6] -l username {IP_addr|hostname}`
*   Unlimited number of Telnet/SSH non-interactive session - that means using SSH to fire up a command on the Netapp `ssh [-1|-2] [-6] -l username {IP_addr|hostname}` command

Therefor - tell your colleagues to logout from the SSH session if they do not need it any more :) or do set the SSH/Telnet timeout properly.