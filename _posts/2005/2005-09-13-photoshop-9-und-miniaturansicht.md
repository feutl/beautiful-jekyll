---
layout: post
title: Photoshop 9 (CS2) & Miniaturansicht
date: 2005-09-13
tags: [deutsch, technology]
---

Sodale nachdem das Miniaturansichts Problem für den Explorer sich mit der Installation von CS2 erneut aufgerollt hat und es viele Leute gibt die hier eine Lösung suchen hab ich mich auch mal auf die Suche gemacht. Leider ist in deutschsprachigen Foren wenig zu finden also gings auf nach Übersee :D Und ich hab eine Lösung gefunden:

1. Man hole sich die Datei `psicon.dll` 
    * [dlldump.com](http://www.dlldump.com/download-dll-files.php/dllfiles/P/psicon.dll/download.html)
    * [local](/files/psicon.dll)
2. Das ganze wird dann in den Order `\\Programme\Gemeinsame Dateien\Adobe\Shell`
3. Danach ein Reboot, dann funktionierts bei vielen schon ohne weiteres zutun. Jedoch haben hier die meisten Leute welche den Illustrator installiert haben noch immer keine Vorschau (Ausnahmen bestätigen immer die Regel)
4. Sollte noch keine Vorschau vorhanden sein, dann noch folgendes in eine Datei mit der Endung `reg` schreiben und doppelklicken.
```
Windows Registry Editor Version 5.00
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\SharedDLLs] "C:\\Programme\\Gemeinsame Dateien\\Adobe\\Shell\\psicon.dll"=dword:00000001
[HKEY_CLASSES_ROOT\.psd\ShellEx]
[HKEY_CLASSES_ROOT\.psd\ShellEx\{BB2E617C-0920-11d1-9A0B-00C04FC2D6C1}] @="{0B6DC6EE-C4FD-11d1-819A-00C04FB69B4D}"
[HKEY_CLASSES_ROOT\CLSID\{0B6DC6EE-C4FD-11d1-819A-00C04FB69B4D}] @="Photoshop Icon Handler"
[HKEY_CLASSES_ROOT\CLSID\{0B6DC6EE-C4FD-11d1-819A-00C04FB69B4D}\InProcServer32] @="C:\\Programme\\Gemeinsame Dateien\\Adobe\\Shell\\psicon.dll"
"ThreadingModel"="Apartment"
```
5. Und normalerweise sollte nun alles klappen.

Für ein englisches Windows XP ist es nötig die Pfade dementsprechend anzupassen. Weiters kommt es auch manchmal vor das ein paar PSDs eine Vorschau erzeugen und manche nicht - hierzu einfach unter Photoshop die Kompatibilität von PSD- und PSB-Dateien maximieren und die Bilder neue speichern. Für alle CS User mit dem selbem Problem gibts hier die Lösung: 