---
layout: post
title: Rebuild the LaunchServices Database
date: 2006-12-11
tags: [deutsch, technology]
---

Wer kennt das Problem nicht, man installiert Programme oder Update Programme auf seinem Apple mit Mac OS 10.4 und wenn man dann auf "Öffnen mit" klickt sieht man manche Programme doppelt darin enthalten.

Der Grund dafür ist, dass ab und zu Programme sich nicht sauber in der LaunchServices Database registriert werden. Doch das ist alles halb so schlimm, um die LaunchServices Database neu zu initialisieren und die doppelten Einträge zu entfernen reicht es im Terminal folgende Zeile einzugeben:

`/System/Library/Frameworks/ApplicationServices.framework/ Frameworks/LaunchServices.framework/Support/lsregister -kill -r -domain local -domain system -domain user`

Danach etwas warten ;) kann ein paar Minuten dauern bis der Terminal Cursor wieder erscheint.