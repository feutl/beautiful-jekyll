---
layout: post
title: VMware Player Network Editor Alternative
date: 2013-03-08
tags: [english, technology]
---

Everybody knows vmnetcfg.exe - but with VMWare Player 5.0 it has gone missing. A lot of instructions can be found how to extract the handy network editor from the Workstation Version or download it from a torrent site.

Much easier is to use the command line - because the well known network editor is still present - but not as a single executable. In this case start cmd.exe and change to the VMWare Players install directory and run in elevated cmd.exe-box

`rundll32.exe vmnetui.dll VMNetUI_ShowStandalone`