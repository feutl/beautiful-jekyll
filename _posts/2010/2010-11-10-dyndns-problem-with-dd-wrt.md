---
layout: post
title: DynDNS Problem with DD-WRT
date: 2010-11-10
tags: [english, technology]
---

Since a few weeks my DD-WRT router running on V24-SP2 is coming up with an annoying log message concerning the DynDNS Service I am using `DYNDNS: Error 'RC_IP_RECV_ERROR' (0x15) when talking to IP server` 

After digging around in the DD-WRT Forum I found some interesting threads trying to figure out where the problem is located

*   [DDNS Errors](http://www.dd-wrt.com/phpBB2/viewtopic.php?t=80136)
*   [08/29/10 - FYI- DynDNS is changing its FREE DynDNS accounts](http://www.dd-wrt.com/phpBB2/viewtopic.php?t=78047)
*   [DynDNS Wiki](http://www.dd-wrt.com/wiki/index.php/DDNS_-_How_to_setup_Custom_DDNS_settings_using_embedded_inadyn_-_HOWTO#DynDNS)
*   [DDNS and DynDns not update](http://www.dd-wrt.com/phpBB2/viewtopic.php?p=497576#497576)

After a lot of good ideas and helpful comments I took the quick route (noted by a forum member) and fixed the problem for me by setting up DynDNS manually:

1.  Go to Setup / DDNS of your DD-WRT router
2.  DDNS Service: Custom
3.  DYNDNS Server: members.dyndns.org
4.  User Name: #yourusername#
5.  Password: #yourpassword#
6.  Host Name: #yourdyndnshostname#
7.  URL: /nic/update?
8.  Additional DDNS Options: --dyndns_system dyndns@dyndns.org --ip_server_name 91.198.22.70:8245 /

The rest stays with the default settings - thats it afters Apply Settings the error should be gone :)