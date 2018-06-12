---
layout: post
title: pfSense auf alter Barracuda NextGen Firewall Hardware
date: 2016-05-04
tags: [deutsch, technology, barracuda]
bigimg: /img/2016/pfsense-open-source-security.png
---

Vor einigen Wochen wurde [pfSense 2.3](https://doc.pfsense.org/index.php?title=2.3_New_Features_and_Changes) veröffentlicht. Neben vielen Features und Änderungen an der Distribution war die bedeutendste ein neues Web-Interface. Darauf fühl ich mich wohl, damit kann ich arbeiten, schließlich konfiguriert das Auge mit ;) Für jene die nicht wissen was [pfSense](https://www.pfsense.org/) ist, hier ein Auszug aus [Wikipedia](https://de.wikipedia.org/wiki/PfSense)

> pfSense ist eine Firewall-Distribution auf der Basis des Betriebssystems FreeBSD und des Paketfilters pf. Die Distribution ist ein Fork vom mittlerweile eingestellten Projekt m0n0wall und wurde 2004 von Chris Buechler und Scott Ullrich ins Leben gerufen.

Eine Testinstallation als virtuelle Maschine ware ohne Probleme möglich und damit war es Zeit pfSense auf echter Hardware laufen zu lassen. Zufällig stand eine [Barracuda NG Firewall F100](https://techlib.barracuda.com/NG61/F101B) herum, die zu diesem Zweck herangezogen werden konnte. 

pfSense stellt eine [NanoBSD Image](https://doc.pfsense.org/index.php/Installing_pfSense#NanoBSD_vs_NanoBSD.2BVGA) zur Verfügung, welches man mit [Win32DiskImager](https://sourceforge.net/projects/win32diskimager/) oder [ähnlichen Tools](https://doc.pfsense.org/index.php/Writing_Disk_Images) direkt auf die Compact Flash Karte aufspielen kann. Da diese Option bei dieser Box nicht funktioniert hat, wählte ich die Installation über einen [MemoryStick mit Serial Console Output](https://doc.pfsense.org/index.php/Installing_pfSense#Installer_ISO_vs_Memstick_vs_Memstick_Serial). 

Kurzum, 20 Minuten später hatte ich der doch älteren F100 neues Leben eingehaucht und pfSense lief und läuft noch immer einwandfrei. Eine Änderung habe ich sofort nach der Installation durchgeführt, nämlich die Nutzung einer Ram Disk eingeschalten.

## Installation

1.  Download und entpacken von pfSense
    *   [Download pfSense](https://doc.pfsense.org/index.php/Installing_pfSense#Download_pfSense)
    *   [Installer ISO vs Memstick vs Memstick Serial](https://doc.pfsense.org/index.php/Installing_pfSense#Installer_ISO_vs_Memstick_vs_Memstick_Serial)
    *   [pfSense-CE-memstick-serial-2.3-RELEASE-i386.img.gz](https://www.pfsense.org/download/mirror.php?section=downloads)
2.  USB Stick erstellen _Hinweis: Die Endung der IMG Datei einfach auf ISO umschreiben und schon funktioniert das schreiben des USB Sticks mit Rufus._
    *   [Writing Disk Images](https://doc.pfsense.org/index.php/Writing_Disk_Images)
3.  Konsolenkabel anstecken und mittels [Putty](http://www.putty.org) oder ähnlichem eine serielle Verbindung aufbauen. _Hinweis: Es müssen die Settings von pfSense verwendet werden auch wenn dadurch die Boot Informationen der F100 unlesbar sind._
    *   [Connecting to the Serial Console](https://doc.pfsense.org/index.php/Connecting_to_the_Serial_Console)
    *   pfSense Console Settings
        ```
        Speed: 115200
        Data Bits: 8
        Parity Bits: None
        Stop Bits: 1
        ```
    *   Barracuda F100 Console Settings
        ```
        Speed: 19200
        Data Bits: 8
        Parity Bits: None
        Stop Bits: 1
        ```
4.  Jetzt gilt es die Fragen des Wizards zu beantworten und geschafft ist die Installation.
    *   [pfSense Default Configuration](https://doc.pfsense.org/index.php/Installing_pfSense#pfSense_Default_Configuration)
5.  Danach würde ich die RAM Disk einschalten und die Console Settings auf die der Hardware abändern. Bei der F100 sind es 19200.
    *   _System > Advanced > Miscellaneous > Ram Disk Settings_
    *   _System > Advanced >Admin Access > Serial Communications_

![CLI Login](/img/2016/pfsense-cli-login.png)
![Dashboard](/img/2016/pfsense-dashboard.png)
![MemDisk](/img/2016/pfsense-memdisk-boot.png)
![RamDisk](/img/2016/pfsense-ram-disk.png)
![reboot](/img/2016/pfsense-reboot.png)
![Serial](/img/2016/pfsense-serial.png)
