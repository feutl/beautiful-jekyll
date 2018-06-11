---
layout: post
title: Schedule to reboot a Windows Machine
date: 2008-06-11
tags: [deutsch, technology]
---

Computer sind Arbeitstiere, und ganz im speziellen Server, trotzdem gehören auch diese Geräte nach speziellen Updates neu gestartet. Diesen Vorgang während der Arbeitszeit zu machen führt sehr oft zu nervenden Klingelorgien des Telefones. Aus diesem Grund macht es Sinn einen Server zu Zeiten neu zu starten in denen keiner die Resourcen dafür benötigt. Meist weil viele der User im Bett liegen und schlafen, natürlich auch der Administrator. Daher muss ein Restart zeitgesteuert passieren und hier bietet Windows die nötigen Bordmittel.

AT – heißt das Command Line Tool. Alle Schalter und Optionen erklärt Microsoft in einem Knowledge Base Eintrag genauer.

Reboot eines Computers um 2 Uhr Morgens
```
C:>at 2:00 shutdown.exe -r -f
```

Die Zeitangaben können im 24 oder 12 Stunden Format gemacht werden, bei zweiterem jedoch nicht AM oder PM vergessen. Mit dem Bordmittel “shutdown.exe” kann der Computer in unserem Fall Rebooten werden und dazu wird der Switch “-r” verwendet. “-f” erzwingt das Beenden aller laufenden Programme. Weiters kann man mit “-t” den Shutdown Prozess verzögern um dem User eine Interaktionszeit zu bieten und mit “-c” kann man den Shutdown Grund kommentieren.
```
C:>at 8:00am shutdown.exe -r -f -t 10 -c “updates”
C:>at 20:00 shutdown.exe -r -f -t 10 -c “updates”
```
