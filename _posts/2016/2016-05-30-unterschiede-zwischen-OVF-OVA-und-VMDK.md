---
layout: post
title: Unterschiede zwischen OVF, OVA und VMDK
date: 2018-05-30
tags: [deutsch, technology]
permalink: /unterschiede-zwischen-ovf-ova-und-vmdk/
---

Immer wieder kommen Besucher vorbei um 2 Posts aus 2011 anzusehen. Anscheinend dürften die Probleme noch nicht ganz behoben sein oder auch immer wieder einmal auftreten. Im Speziellen handelt es sich um die Handhabung von OVA und OVF Dateien.

*   [The OVF Descriptor File could not be parsed](http://www.feutl.com/the-ovf-descriptor-file-could-not-be-parsed/)
*   [The OVA Package Name does not match the OVF File inside it](http://www.feutl.com/the-ova-package-name-does-not-match-the-ovf-file-inside-it/)

Aber was ist eine OVF bzw. OVA Datei überhaupt?

## Open Virtualization Format

> Das Open Virtualization Format (OVF; deutsch Offenes Virtualisierungsformat) ist ein offener Standard, um Virtual Appliances oder allgemeiner Software, die in virtuellen Maschinen läuft, zu verpacken und zu verteilen. Entwickelt wurde dieser Standard von der Distributed Management Task Force (DMTF). Der Standard beschreibt ein „offenes, sicheres, portables, effizientes und erweiterbares Format für die Verpackung und Verteilung von Software, die in virtuellen Maschinen läuft“. Der OVF Standard ist nicht auf bestimmte Hypervisoren oder Prozessor-Architekturen beschränkt. Die Einheit, die in der Verpackung und Verteilung stattfindet, wird OVF Package genannt. Ein OVF Package kann ein oder mehrere virtuelle Systeme enthalten, von denen jedes in eine virtuelle Maschine eingespielt werden kann. Quelle: [Wikipedia](https://de.wikipedia.org/wiki/Open_Virtualization_Format)

## Open Virtualization Archive

Eine OVA Datei ist die OVF Ordnerstruktur gepackt in ein [tar-Archiv](https://de.wikipedia.org/wiki/Tar). Somit erhält man eine einzige Datei welche man einfacher verschieben, weitergeben, ablegen oder nuthen kann als die ganze OVF Ordnerstruktur. Ein weiterer Vorteil von tar-Archiven ist die Möglichkeit diese zu [komprimieren](https://de.wikipedia.org/wiki/Datenkompression). Ein großer Nachteil ergibt sich, wenn das Archiv einen Fehler aufweißt, dann ist auch meist der Inhalt unwiederbringlich verloren.

## Virtual Machine Disk

[VMDK](https://en.wikipedia.org/wiki/VMDK) (Virtual Machine Disk) ist ein Container-Format welches virtuelle Festplatten, genutzt von virtuellen Maschinen wie VMWare Workstation oder [Virtualbox](https://www.virtualbox.org/), beschreibt. Entwickelt wurde das Format von [VMWare](https://www.vmware.com) für die eigenen Produktpalette, gilt jedoch seit einigen Jahren als offenes Format und wird auch im OVF genutzt.