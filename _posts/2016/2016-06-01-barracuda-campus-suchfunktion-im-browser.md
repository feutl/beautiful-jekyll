---
layout: post
title: Barracuda Campus Suchfunktion im Browser
date: 2016-06-01
tags: [deutsch, technology]
bigimg: /img/2016/barracuda-campus.png
---

Moderne Browser bieten einem die Möglichkeit direkt in der Adressleiste Suchbegriffe einzugeben um damit seine bevorzugte Suchseite zu füttern. Man kann jedoch auch auf anderen Seiten direkt nach Informationen suchen. So liefert die Eingabe [de.wikipedia.org phion](https://de.wikipedia.org/wiki/Phion) (wichtig copy'n'paste funktioniert hier nicht) das direkte Suchergebnis auf [Wikipedia.de](https://de.wikipedia.org)

![Barracuda Campus Search Engine](/img/2016/barracuda-campus-search-engine.png)

Dieses Verhalten ist natürlich anpassbar und findet sich in Chrome unter Settings > Manage search engines (chrome://settings/searchEngines). Andere Browser wie Firefox und Co haben ähnliche Möglichkeiten unter Einstellungen.

![Barracuda Campus Search Engine Example](/img/2016/barracuda-campus-search-engine-example.png)

Wer [campus.barracuda.com](https://campus.barracuda.com) zum Nachschlagen verwendet kann auch diesen in die Adressleisten-Suche integrieren. Einfach eine neue Suche hinzufügen. Der Name ist zum Wiederfinden, das Keyword nutzt man später um die Suche gefolgt von einem Leerzeichen in der Adressleiste zu aktivieren. Was man noch braucht ist die richtige URL mit den nötigen Parametern. Diese baut sie für den Barracuda Campus wie folgt zusammen

```
https://campus.barracuda.com/search/product/11/48529411/?q=release+notes

Base URL: https://campus.barracuda.com/search/
Search Type: product/
Product ID: 11
Firmware ID: 48529411/
Search Term: ?q=keyword</pre>
```

In diesem Beispiel suchen wir innerhalb des Produktes Barracuda NextGen Firewall F (ID 11) und der Firmware Version 7.0 (ID 48529411). Die selbe Suche für die Firmware Version 6.2 würde die ID 46759938 nutzen. Diese Informationen sucht man sich am einfachsten über die URL heraus, nachdem man eine Suche abgesetzt hat.

Nun eine Liste von möglichen URLs für den Suchfunktion direkt im Browser. Namen und Keywords könnt ihr natürlich selbst wählen

*   Alle Produkte, alle Software Versionen (gesamter Campus) `https://campus.barracuda.com/search/?q=%s`
*   NextGen Firewall F, alle Software Versionen `https://campus.barracuda.com/search/product/11/?q=%s`
*   NextGen Firewall F, Software Version 7.0 `https://campus.barracuda.com/search/product/11/48529411/?q=%s`
*   NextGen Firewall F, Software Version 6.2 `https://campus.barracuda.com/search/product/11/46759938/?q=%s`
*   NextGen Firewall X, alle Software Versionen `https://campus.barracuda.com/search/product/69/?q=%s`