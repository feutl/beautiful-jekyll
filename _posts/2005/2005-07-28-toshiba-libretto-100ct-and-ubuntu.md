---
layout: post
title: Toshiba Libretto 100CT & Ubuntu
date: 2005-07-28
image: /img/2007/libretto-thumb.jpg
tags: [deutsch, technology]
---

Vor einer kleinen Ewigkeit hat ein [BSD-Foren.de](http://www.bsd-foren.de/) Kollege und ich versucht eine Anleitung zu verfassen um auf einem Libretto 100CT ein Unixoides OS ans Laufen zu bringen. Mein persönliches Ziel war, ohne Nutzung eines 2t PCs oder externen Laufwerken das OS zu installieren.

Nach langen Versuchen erkannten wir, dass es nicht viele Betriebsysteme gibt die mit Diskettenkontroller des Libretto umgehen können. Weiteres Kriterium für mich war damals, dass automatisch erkannt wird das ein PCMCIA Kontroller vorhanden ist. Auf Grund dessen sollte die Installationsroutine auch nachfragen ob man das PCMCIA Gerät für die Installation wechseln will bzw. ein Möglichkeit bieten die Installation über ein anderes PCMCIA Gerät durchzuführen.

FreeBSD 4.11 war es damals und der Wikieintrag mit Infos findet man hier:

[Toshiba Libretto 100CT & FreeBSD 4.11](http://wiki.bsdforen.de/index.php/Toshiba_Libretto_100CT)


Doch aus reiner Neugier und weil mir Ubuntu so gut gefüllt dacht ich mir vor kurzen ob man nicht auch Ubuntu installieren kann. Vielleicht fragen sich viele warum ich ned Debian Sarge oder ähnliches nehme! Und ich sage ich weiß? es nicht - vielleicht weil ich mir erhoffe, dass einige Pakete besser vorkonfiguriert sind oder einfach weil ich die CD daheim hatte.

Nun mehr zum Ubuntu Libretto ... 

Das ganze vorhaben startet man am besten mit einem alten PC und einem 3,5" to 2,5" IDE Adapter. Danach baut man mal die Platte vom Libretto aus und versucht sie mal am anderen Rechner ans laufen zu bringen.

Wenn die HDD vom Bios erkannt wird dann einfach mal von der Ubuntu CD starten und am besten die Server Version von Ubuntu installieren. Alles andere wäre Folter für die Festplatte und unnötig.

Nachdem die Installationsroutine alle Dateien auf die HDD geschaufelt hat und den Reboot durchfüren will einfach alles abhängen und die HDD wieder in den Libretto. Nun werden alle Pakete installiert und konfiguriert.

Danach sollte man PCMCIA ans laufen bringen, dazu muss die Platte nochmal an den StandPC und gebootet werden. Dann einfach die nötigen Pakete installieren. Wer seine Internetleitung schonen will oder gar kein Breitband hat der installiert nebem PCMCIA-Support auch gleich das Package:

`laptop-mode, apmd, X.org, xdm, fvwm` (als windowmanager wenn man will)

Nun wieder die Platte in den Libretto und alle Pakete neu konfigurieren, weil sie ja auf den StandPC optimiert sind (weil ja dort installiert).

`dpkg-reconfigure --all` ist in diesem Fall dein Freund. Das ganze dauert dann eine halbe Ewigkeit, aber nicht weggehehn, ab und zu sind ein paar Fragen zu beantworten.

Danach gehts ans eingemachte, X.org wird noch nicht starten da der Libretto ein Sonderformat für das Display hat und auch die Grafikkarte mehr liebe benötigt.

Das ganze werd ich heut Abend machen und hoffe morgen berichten zu können, dass alles funktionert :D