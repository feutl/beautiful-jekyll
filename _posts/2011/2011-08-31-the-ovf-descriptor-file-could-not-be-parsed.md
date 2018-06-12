---
layout: post
title: The OVF Descriptor File could not be parsed
date: 2011-08-31
tags: [english, technology]
---

It is not ending at all - the series of problems using Cisco OVAs within my VMWare Workstation installation. After solving some minor issues I found out that VMWare got shipped with a pretty old [OVF-tool](https://developercenter.vmware.com/tool/ovf/3.5.2). Hitting to the VMWare site and downloading the new one took me one stop closer.

The OVA can be directly converted to a VMWare Virtual Appliance by using ovftool.exe (located in the program directory of ovftool). It is pretty straight forward

`ovftool.exe <location of the ova file> <location and name of the VMX file>`

After that, the ovftool starts creating and converting any OVA to a VMWare Virtual Appliance. In the meantime you can read through the [ovftool documentation](https://www.vmware.com/support/developer/ovf/ovf21/ovftool-210-userguide.pdf) - it is a very amazing tool at all.