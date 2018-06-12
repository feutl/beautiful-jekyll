---
layout: post
title: The OVA Package Name does not match the OVF File inside it
date: 2011-08-29
tags: [english, technology]
---

Downloaded a OVA file and tried to import it into my VMWare Workstation and if something can go wrong - it does.

`the ova package name does not match the ovf file inside it` was the error message, after some [searching](https://communities.vmware.com/message/1674297?tstart=14) I found out that a OVA is nothing else than a compressed tar file with another ending but includes the OVF and VHD files.

Using 7-zip to look into it I found the name of the OVF and renamed the OVA to the same name - voila - it works :)