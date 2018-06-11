---
layout: post
title: PNG Farbunterschiede im Web - einfache Lösung
date: 2007-05-03
tags: [deutsch, technology]
---

Zu aller erst sollte erwähnt werden, dass dies eine schnelle und einfach Lösung darstellt wenn du deine PNG Dateien mit Photoshop gespeichert hast und noch immer zugriff auf eine Version hast. Unter Umständen kann man diese Lösung auch mit anderen Bildbeartbeitunstools vollziehen doch bezieht sich die Anleitung hier auf Photoshop CS2.

Das Problem mit PNGs und der unterschiedlichen Farbwiedergabe gegenüber anderen Bildern (zB: JPG) oder HEX Color Werten besteht schon seit langer Zeit. Immer wieder stößt man auf das Problem und Leute verschwenden Stunden an Arbeit ohne eine Lösung zu finden. Einzige Lösung für viel war der Einsatz von GIF Dateien anstatt von PNG. Nicht gerade der beste Weg. Auftreten tut dieses Problem durch die Gamma Korrektur die durchgeführt wird, auf Grund der META Daten im PNG File. Wobei die META Daten an sich nicht das Problem sind, eher die Tatsache, dass manche Browser sie interpretieren und andere wieder nicht. Die Folge sind unterschiedliche Darstellungen eines PNGs in versch. Browsern. So lange kein JPG oder ein anders File ohne dieser META Daten dem gegenübersteht fällt es eigentlich niemandem auf. Es gibt einige 3rd Party Lösungen um diese Gamma Korrekturen durchzuführen.

Zwei dieser Programme waren [TweakPNG](http://entropymine.com/jason/tweakpng/) und [PNGCRUSH](http://pmt.sourceforge.net/pngcrush/). Einmal Windows und einmal eine DOS oder Unix/Linux Shell Applikation. Nach einer Weile fand sich auch eine Möglichkeit diese META Daten mit Photoshop CS2 zu betrachten und zu verändern.

Nach dem man ein PNG File gespeichert hat schließt man es und öffnet man es erneut (dadurch geht man sicher, dass die META Daten auch vorhanden sind). Nach dem Öffnen navigiert man zu `File / File Info ...` Danach wechselt man in dem autauchenden Fenster auf `Advanced` und entfernt den Eintrag `Adobe Photoshop Properties (photoshop, http://ns.adobe.com/photoshop/1.0)` Nach einem OK speichert man die Datei erneut.

Von nun an sollte die Gamma Korrektur auf Grund der META Informationen verschwunden sein und PNG Farben mit denen von JPG Bildern zusammenstimmen. Wichtig zu wissen ist, dass nach einem Öffnen und Modizfieren der Datei und einem erneuten Speichern diese META Daten wieder in die Datei geschrieben werden könnten.

Ein einfacher Fix für ein nervenaufreibendes Problem ;) und auch ich bin nur durch Zufall über die Lösung gestolpert. Gefunden in [polar bear lamps blog: PNG color mismatch on the web: an easy fix](http://www.polarbearlamps.net/2007/04/png_color_mismatch_on_the_web.html) und hier aus dem Englischen frei übersetzt. Die Quelle dieses Blogeintrages hat noch weiter Anforschung zu diesem Thema angestellt. Das Ergebnis für Mac User heißt [GammaSlamma](http://www.plasticated.com/GammaSlamma-1.1.dmg) by [Shealan Forshaw](http://www.shealanforshaw.com/gammaslamma-11-update-now-available/). Einfach per Drag & Drop und fertig - noch einfacher gehts eigentlich gar nicht.