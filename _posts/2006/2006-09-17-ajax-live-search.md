---
layout: post
title: AJAX Live Search
date: 2006-09-17
tags: [deutsch, technology]
---

Wer kennt es nicht - man gibt ein paar Buchstaben in ein Textfeld ein und unter dem Textfeld klappt ein kleines Fenster auf das einem Vorschläge liefert nach was man suchen kann. Noch schöner ist, wenn man noch genau diese Vorschläge bekommt, für welche man auch wirklich Ergebnisse bekommen kann.Was braucht man dazu:

*   [Prototype](http://prototype.conio.net/)
*   [Sciptaculous](http://script.aculo.us/)
*   Zeit ;)

Der [Artikel von eDevil](http://edevil.wordpress.com/2005/12/12/live-search/) beschreibt sehr gut wie man vorgehen muss um eine solche Suche aufzubaun und benötigt eigentlich keine weitere Erklärung. Aufpassen muss man unbedingt wenn man die möglichen Suchwörter direkt aus der Datenbank ausliest.

*   Unbedingt mit LIMIT im SQL Statement arbeiten. Dies bringt für den User zwar nicht alle Möglichkeiten sofort zum Vorschein - erhöht aber die Reaktionszeiten ungemein.
*   DISTINCT sollte man wenn möglich auch im SQL Statement einbauen um nicht doppelte Vorschläge zu bekommen.
*   Wenn man die Anzahl der Suchergebnisse mit LIMIT nicht verringern will, wäre es vielleicht sinnvoll die Suche erst aber zB: dem 3ten eingegeben Zeichen anzufangen.