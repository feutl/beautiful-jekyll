---
layout: post
title: Proxy Auto-Configuration and its challenges
date: 2011-07-01
tags: [english, technology, cisco]
---

I was a fan of WCCP for setting up transparent proxy within a network - it always seemed the easiest way but all together it only seemed like that. A lot of problems came up in the past few month on customer sides and within my installation so I decided to give Proxy Auto-Configuration a try.

Biggest benefit of using PAC (Proxy Auto-Configuration) is: "You get rid of transparent proxy." That makes life easier - but before I had to learn a lot of stuff the hard way.

## Rollout the URL for the PAC File without touching the client

2 Options are available - DNS and Option 252 for DHCP 

Easiest way is DHCP and the configuration therefore is straight forward. Extend your DHCP configuration with the option 252 and put the URL for the PAC file as a value into. The client fetches with the next renew of the DHCP settings also the proxy information.

DHCP has a higher priority than DNS: if DHCP provides the WPAD URL, no DNS lookup is performed. Notice that Firefox and Chrome do not support DHCP, only DNS. 

Next step is to set up DNS for the browsers lacking DHCP support. It's also straight forward - redirect any request for wpad.yourinternaldomain.com to the PAC file server. The browser is going to fetch the file wpad.dat (which is our PAC file) from the file server.

## Verify your Clients

Very important for your client PCs and/or applications is that they are set to auto-detect proxy settings from your network. If this is not set up - you have to touch the client or use some kind of scripting to set that on your browsers.

## PAC file hosting

One challenge could be the PAC file hosting. If you use a webserver - it is important that every PAC file (nevertheless if it is called proxy.pac or wpad.dat) sent to the client gets the right MIME type. The MIME type of the configuration file must be "application/x-ns-proxy-autoconfig". 

If you are using DNS to get the PAC file - every client is requesting the wpad.dat file from the URL mentioned above on port 80.

## PAC file hosting with Cisco Ironport Web Appliance

If you are using a Cisco Ironport S-Series or Web Appliance - a lot of things get handled by the Ironport itself. MIME type is set right and a few other things which we are talking right now. 

Ironports PAC file hosting lets you specify a port for the PAC file service - per default 9001\. If you use DNS - the PAC file service has to listen on port 80 as well. That is not a problem as long as you are not using port 80 for your web proxy service and your AsyncOS Version is 7.x Just add the port 80 to the PAC file service and submit the changes. 

Next step is to upload your PAC file - the PAC File can have any name as long as you can remember it and use it right if you set up your DHCP settings. Ironport also supports multiple PAC files as long as they have a different name. That's it if you can use DHCP - every DHCP pool within your network could fetch a different PAC file from the same Ironport Appliance.

Talking about DNS - you need to host wpad.dat files - Ironport is helping out. In the section "Hostnames for Serving PAC Files Directly" you can set up a GET hostname (the URL the client is using to access the PAC hoster) and choose a PAC file from your uploaded one and Ironport is renaming it on demand for the client requesting.

For example, if you enter wsa.example.com in the Hostnames field and pacfile1.pac in the Default PAC File for “Get/” Request through Proxy Port field, then requests for http://wsa.example.com/ fetch pacfile1.pac and requests for http://wsa.example.com/default.pac fetch default.pac.

## Additional Information

*   Mozilla DHCP / DNS Bug [https://bugzilla.mozilla.org/show_bug.cgi?id=356831](https://bugzilla.mozilla.org/show_bug.cgi?id=356831)
*   Better Proxy Settings… Bluecoat, wpad, proxy.pac & dhcp option 252 [http://www.linickx.com/960/better-proxy-settings-bluecoat-wpad-proxypac-dhcp-option-252](http://www.linickx.com/960/better-proxy-settings-bluecoat-wpad-proxypac-dhcp-option-252)
*   Wikipedia WPAP [http://en.wikipedia.org/wiki/Web_Proxy_Autodiscovery_Protocol](http://en.wikipedia.org/wiki/Web_Proxy_Autodiscovery_Protocol)
*   Proxy Auto-Configuration [http://en.wikipedia.org/wiki/Proxy_auto-config](http://en.wikipedia.org/wiki/Proxy_auto-config)
*   Ironport KB [https://ironport.custhelp.com](https://ironport.custhelp.com/cgi-bin/ironport.cfg/php/enduser/std_adp.php?p_faqid=1543&p_created=1266254164&p_sid=rQWXESxk&p_accessibility=0&p_redirect=0&p_srch=1&p_lva=471&p_sp=cF9zcmNoPTEmcF9zb3J0X2J5PSZwX2dyaWRzb3J0PSZwX3Jvd19jbnQ9MiwyJnBfcHJvZHM9NDkmcF9jYXRzPTAmcF9wdj0xLjQ5JnBfY3Y9JnBfc2VhcmNoX3R5cGU9YW5zd2Vycy5zZWFyY2hfbmwmcF9wYWdlPTEmcF9zZWFyY2hfdGV4dD13cGFk&p_li=cF91c2VyaWQ9MXJvblAwcnQmcF9wYXNzd2Q9Zm8wQmE1&p_topview=1)
*   Proxy Auto-Detect [http://blog.freyguy.com/archives/2006/03/01/proxy-auto-detect-ie-and-firefox/](http://blog.freyguy.com/archives/2006/03/01/proxy-auto-detect-ie-and-firefox/)
*   Automatic proxy HTTP server configuration in web browsers [http://homepage.ntlworld.com./jonathan.deboynepollard/FGA/web-browser-auto-proxy-configuration.html](http://homepage.ntlworld.com./jonathan.deboynepollard/FGA/web-browser-auto-proxy-configuration.html)
*   Understanding Autoconfiguration Files [http://web.archive.org/web/20040810122331/http://developer.netscape.com/docs/manuals/proxy/adminux/autoconf.htm](http://web.archive.org/web/20040810122331/http://developer.netscape.com/docs/manuals/proxy/adminux/autoconf.htm)