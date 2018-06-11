---
layout: post
title: Die Zeitspanne "Tick"
date: 2007-03-01
tags: [deutsch, technology]
---

Ich arbeite jetzt ja seit Wochen wieder mehr mit ASP.net, da kommt man schon auf nette Sachen drauf ;) Leider bin ich einfach zu lusch um das immer zu posten, trotzdem hier mal ein kleiner Beitrag zur Zeiteinheit Tick.

Im .Net Framework folge die Zeitmessung in Einheiten zu 100 Nanosekunden, dem sogenannten Tick. Start dieser Zeitmessung war der 1.1.00001 und die Anzahl der Ticks seit Beginn dieser Zeitrechnung können in einer long Variable gespeichert werden. Somit sollt sich eine Zeitrechnung bis zum Jahre 9999 ausgehen.

Was aber nun interessanter ist, wie kommt man zu den aktuellen Ticks bzw. wie kann man Ticks in ein Datum / Zeit Format zurückrechnen?

* Aktuelle Zeit: `Console.WriteLine(DateTime.Now.Ticks);`
* Ticks in Datum / Zeit verwandeln: `DateTime actualDate = new DateTime(631452984963219664); Console.WriteLine(actualDate.ToString());`
* Ausgabe: `30.12.2001 08:41:36`