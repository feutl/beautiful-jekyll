---
layout: post
title: Limit and Offset SQL Pagination
date: 2006-09-08
tags: [deutsch, technology]
---

Man hat 1000te Einträge in einer Datenbank. Alle auf einmal anzuzeigen würde den Browser und meiste auch die Internetleitung überfordern. Darum greifen viele Leute bei ihren Website Projekten auf eine alt bewährte Art zurück.

Sie lassen nur eine gewissen Anzahl von Einträgen anzeigen und den User lassen sie einfach nach vorne oder zurück blättern. (siehe Google)

Doch wie lässt man solche in Problem in der Praxis. Man kann alle Einträge in ein Array, Resultset, eine Hashtable oder ähnliches laden und dort dann nur die Werte ausgeben die man benötigt. Ein paar for oder while Schleifen sind hier dann meist im Einsatz.

Doch warum nicht den Traffic an der richtigen stelle beschränken und den Programmieraufwand reduzieren?

Die richtige Stelle meiner Meinung ist in diesem Fall bei SQL anzusetzen: Hilfreich dabei ist die Möglichkeit das LIMIT Keyword mit OFFSET zu kombinieren.

LIMIT reduziert die zurück gebenen Results eines SQL Queries: `SELECT column FROM table LIMIT 10`

Um nun alle Einträge von 1 bis 10 zu bekommen brauchen wir nichts großartiges ändern. Um jedoch die Einträge von 11 bis 20 zu bekommen nutzen wir das OFFSET Keyword: `SELECT column FROM table LIMIT 10 OFFSET 10`

Hexerei perfekt und Traffik gespart, Geschwindigkeit angehoben und den User glücklich gemacht. Was natürlich keiner von den Usern weiß: "Wir haben uns (dem Programmmierer) Arbeit gespart ;)