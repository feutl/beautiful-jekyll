---
layout: post
title: wpad DNS resolution not working
date: 2011-07-07
tags: [english, technology]
---

After rolling out the proxy settings within my network, there is another nice feature I stumbled upon: "Networks using Windows 2003 and/or 2008 Servers as a DNS do or can block wpad request by default." 

Nice if you do not use it - but kinda hard to find if you need it and don't know it. 

Windows 2008 is straight forward to configure and Microsofts KB is helping. Windows 2003 is a different story. I found [Chris Dents](http://www.indented.co.uk/index.php/2009/05/21/windows-2003-dns-global-query-block-list/) homepage to address the issue because Microsofts KB ist nor very useful. I looked into the registry and surprisingly the so called global query block list was disabled (as the handbook says but why does it now work). 

Nevertheless - without deleting the entries for wpad and restarting the DNS Server service the wpad URL wasn't able to be resolved.

So be aware of that :)

## Enabling or Disabling the Global Query Block List

* Key: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNS\Parameters
* Name: EnableGlobalQueryBlockList
* Type: REG_DWORD (DWORD Value)
* Data: Enable: 1; Disable: 0

The default is disabled.

## Managing the Global Query Block List

* Key: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNS\Parameters
* Name: GlobalQueryBlockList
* Type: REG_MULTI_SZ (Multi-String Value)
* Data: wpad isatap