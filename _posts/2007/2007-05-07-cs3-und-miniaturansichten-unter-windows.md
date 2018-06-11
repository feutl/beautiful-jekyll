---
layout: post
title: CS3 und Miniaturansichten unter Windows
date: 2007-05-03
tags: [deutsch, technology]
---

[Adobe Creative Suite 3](http://www.adobe.com/products/creativesuite/) befindet sich nun am Markt. Für Windows User beginnt somit die Suche nach Lösungen um die Photoshop Icon im Explorer durch Vorschaubilder zu ersetzen. Ein Blogleser namens __Lexy__ hat per Kommentarfunktion heute verkündet, dass die beschriebene Vorgehensweise des Artikeles [Photoshop 9 (CS2)](/2005-09-13-photoshop-9-und-miniaturansicht.md) auch bei der Creative Suite 3 funktioniert.

Mangels Windows PCs und CS3 konnte ich das zwar noch nicht testen doch ich glaube meinen Kommentatoren ;) werde aber sobald als möglich auch CS3 mit Vorschaubildern probieren. Beschreibung gibts weiter unten im Artikel bzw. nach dem Sprung.

Mit dieser Anleitung werden nun CS2 und CS3 unterstützt wie auch die Betriebssysteme Windows XP und Windows Vista. Wer noch Photoshop 8 einsetzt findet im Artikel [Photoshop 8 Miniaturansichten](/2005-03-21-photoshop-8-und-miniaturansicht.md) die nötige Hilfe.

1.  Man hole sich die Datei _psicon.dll_ [direkt hier](/files/psicon.dll) oder die aktuelleste Version von [dlldump.com](http://www.dlldump.com/download-dll-files.php/dllfiles/P/psicon.dll/download.html)
2.  Das ganze wird dann in den Order _\ProgrammeGemeinsame DateienAdobeShell_
3.  Danach ein Reboot, dann funktionierts bei vielen schon ohne weiteres zutun. Jedoch haben hier die meisten Leute welche den Illustrator installiert haben noch immer keine Vorschau (Ausnahmen bestätigen immer die Regel)
4.  Sollte noch keine Vorschau vorhanden sein, dann noch folgendes in eine Datei mit der Endung _reg_ schreiben und doppelklicken. Oder die Datei [hier](/files/psp.reg "PSP Registry Import") herunterladen!
```
Windows Registry Editor Version 5.00
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\SharedDLLs]
"C:\\Programme\\Gemeinsame Dateien\\Adobe\\Shell\\psicon.dll"=dword:00000001
[HKEY_CLASSES_ROOT\.psd\ShellEx]
[HKEY_CLASSES_ROOT\.psd\ShellEx\{BB2E617C-0920-11d1-9A0B-00C04FC2D6C1}]
@="{0B6DC6EE-C4FD-11d1-819A-00C04FB69B4D}"
[HKEY_CLASSES_ROOT\CLSID\{0B6DC6EE-C4FD-11d1-819A-00C04FB69B4D}]
@="Photoshop Icon Handler"
[HKEY_CLASSES_ROOT\CLSID\{0B6DC6EE-C4FD-11d1-819A-00C04FB69B4D}\InProcServer32]
@="C:\\Programme\\Gemeinsame Dateien\\Adobe\\Shell\\psicon.dll"
"ThreadingModel"="Apartment"
```
5.  Und normalerweise sollte nun alles klappen.

Für ein englisches Windows XP / Vista ist es nötig die Pfade dementsprechend anzupassen. Weiters kommt es auch manchmal vor das ein paar PSDs eine Vorschau erzeugen und manche nicht - hierzu einfach unter Photoshop die Kompatibilität von PSD- und PSB-Dateien maximieren und die Bilder neue speichern. Für alle CS User mit dem selbem Problem gibts hier die Lösung: [Photoshop 8 & Miniaturansicht](/2005-03-21-photoshop-8-und-miniaturansicht.md)