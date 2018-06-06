---
layout: post
title: NextGen Firewall 7.0.0 build 672
date: 2016-06-07
tags: [deutsch, technology, barracuda]
---

Nachdem das [Release 7.0.0-664](http://www.feutl.com/7-0-0-fur-barracuda-nextgen-firewall-f-veroffentlicht/) zurückgezogen wurde ist eine neue Version seit gestern wieder online. Auch NextGen Admin zeigt für alte und schon 7.0.0 Firewalls ein Update auf die **Version 7.0.0.-672** an. Damit sind Fehler behoben die nicht hätten passieren sollen, aber trotzdem passiert sind ;)

[Release Notes 7.0.0](https://campus.barracuda.com/product/nextgenfirewallf/article/NGF70/ReleaseNotes/)

## Improvements included in version 7.0.0 build 672

> **RIP/OSPF/BGP** 
> Enabling OSPF by setting **Run OSPF Router** to **yes** on the **OSPF/RIP/BGP Settings** page now works as expected. (BNNGF-39115)
> 
> **VPN** The VPN service now works as expected on F-Series Firewalls and Control Centers using 32-bit  kernels: NextGen Firewall F10, F15, F100, F101, F200, F201, F300 and F301  (BNNGF-39297) 
> 
> IPsec IKEv1 tunnels using AES256 encryption and SHA256 hashing now work as expected. (BNNGF-39297, BNNGF-39295)
> 
> **Firewall** 
> Connection object failover and loadbalancing policies now work as expected when the first entry is a network interface. (BNNGF-39287)
> 
> Application Control for SSL encrypted traffic now works as expected when used in combination with IPS and SSL Interception. (BNNGF-39221)
> 
> Improvements to the IP defragmentation handling of acpfctrl monitor mode. (BNNGF-39394)
> 
> **Control Center** NextGen Control Centers in Azure using the old VFC610 model names can now be updated. (BNNGF-39040)
> 
> CC Database no longer causes problems logging in to the Control Center. (BNNGF-39285)
