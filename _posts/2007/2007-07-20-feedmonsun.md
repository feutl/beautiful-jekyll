---
layout: post
title: FeedMonsun
date: 2007-07-20
tags: [deutsch, technology]
---

![FeedMonsun](/img/2007/feedmonsun_shot1.png)

[Try FeedMonsun Now](http://ojs.at:8080/Feed_Monsun)

## Was ist FeedMonsun
FeedMonsun ist eine Online RSS Aggregation Application entwickelt von [Florian Beer](http://blog.no-panic.at) und mir als Uni Projekt für das Fach "Programmierung Verteilter Systeme". Das Ziel war mittels eines kleinem Projektes die Grundzüge von J2EE kennen zu lernen. Diese Aufgabe und die Tatsache das wir gerade RSS entdeckt haben brachte uns die Idee zur Entwicklung dieser Applikation.

Leider kam dieses Version von FeedMonsun nie über das Pre-Alpha Stadium hinaus. Die Core-Funktionen sind verfügbar und alle Anforderungen unseres Lektores waren mehr als erfüllt worden. Leider fehlte uns danach die Zeit für die Weiterentwicklung.

Neben den Core-Funktionen waren weiter Features geplant:
* User-Registration
* Friendly URLs
* OPML Support
* Republishing the aggregated RSS Feed

## Funktionsweise von FeedMonsun
FeedMonsun wurde mittels JSP und J2EE entwickelt. Die Core-Funktionalität wird von Servlets bereitgestellt. Für die nötigen RSS Funktionalitüt wird die Library [Informa](http://informa.sourceforge.net/) eingesetzt. Das Userinterface wurde mit etwas Javascript aufgepeppt und in Zukunft wäre AJAX also Feature geplant.

Das Hauptziel bei der Entwicklung war eine Easy-to-Use UI. Aus diesem Grund is auch keine Registrierung nötig. Man muss nur seine RSS Feed URLs eintragen, auf "engage" klicken und alles wird erledigt. Wichtig um auf die zusammengefassten Feeds wieder zugreifen zu können, ist das Niederschreiben der eigenen User ID.

Als Beispiel: In der Adressleiste findet man _?u=f0e6810a582b67485523d2cb9b191639_ als persönliche ID. Folglich sieht die komplette URL zum Wiederaufrufen der eigenen Feeds wie folgt aus: [http://ojs.at:8080/Feed_Monsun/Feeds?u=f0e6810a582b67485523d2cb9b191639](http://ojs.at:8080/Feed_Monsun/Feeds?u=f0e6810a582b67485523d2cb9b191639)

Nicht unbedingt die schönste URL aber quick and dirty ;) Ein spezieller Danke geht noch an [Oliver](http://ojs.at/), der uns den Java Webserver zur verfügung stellt.