---
layout: post
title: RSS Feed direkt an Feedly übergeben
date: 2016-05-21
image: /img/2016/rss.png
tags: [deutsch, technology]
---

Originally distributed by the Mozilla Foundation under a MPL/GPL/LGPL tri-license.[/caption] Wer noch von der alten Schule ist und RSS Reader verwendet kennt [Feedly](https://feedly.com) bestimmt. Er ist neben vielen anderen guten RSS Readern ein direkter Nachfolger des eingestellten [Google Reader](https://www.google.com/reader/about/).

Das hinzufügen von RSS Feeds in Feedly funktioniert gut, per Copy & Paste in die Suchbox. Vor nicht all zu langer Zeit funktioniert das Abonnieren von Webseiten noch per Klick auf ein RSS Icon das direkt in der Adressleiste des Browsers angezeigt wurde, so die Webseite RSS unterstützte.

Leider wird das gute alte RSS Icon schon lange nicht mehr in den Browsern standardmäßig angezeigt, es benötigt meist eine Extension und bei vielen dieser ist zum Beispiel Feedly nicht integriert. Damit keine One-Click Option.

Jedoch kann man mit wenig Aufwand das Problem lösen. Wer die [offizielle Google Erweiterung für Chrome](https://chrome.google.com/webstore/detail/rss-subscription-extensio/nlbjncdgjeocebhnmkbbbdekmmmcbfjd?utm_source=chrome-app-launcher-info-dialog) verwendet kann dort auch eigene Feed Reader hinzufügen.

1. Extension installieren
2. Optionen öffnen
3. Feed Reader hinzufügen

![RSS Extension Option](/img/2016/rss-extension-option.png)

Die URL um Feedly aufzurufen und den RSS Feed zu übergeben sieht folgendermaßen aus

`https://feedly.com/i/subscription/feed/%s`

`%s` wird durch den RSS Feed ersetzt, somit kann man URL in angepasster Form auch für andere RSS Extensions einsetzen.

## Was ist RSS?

> RSS sind Dateiformate für Web-Feeds. Sie zeigen Änderungen auf Websites, z. B. auf News-Seiten, Blogs, Audio-/Video-Logs etc. Das Backronym steht aktuell für Really Simple Syndication (etwa sehr einfache Zusammenfassung), vormals waren bereits andere Bedeutungen gegeben. RSS-Dienste werden meist auf speziellen Service-Websites angeboten, sogenannten RSS-Channels. Ein gewöhnlicher RSS-Channel versorgt den Adressaten, ähnlich einem Nachrichtenticker, mit kurzen Informationsblöcken, die aus einer Schlagzeile mit Textanriss und einem Link zur Originalseite bestehen. Zunehmend werden aber auch komplette Inhalte klassischer Webangebote ergänzend als Volltext-RSS bereitgestellt. Die Bereitstellung von Daten im RSS-Format bezeichnet man auch als RSS-Feed, von engl. to feed – im Sinne von füttern, einspeisen, zuführen. Wenn ein Benutzer einen RSS-Channel abonniert hat, so sucht der Client in regelmäßigen Abständen beim Server nach Aktualisierungen im RSS-Feed. Quelle: [Wikipedia](https://de.wikipedia.org/wiki/RSS_(Web-Feed))