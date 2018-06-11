---
layout: post
title: Internetgateway unter Windows XP entfernen
date: 2006-09-29
tags: [deutsch, technology]
---

Windows XP hat die nette Eigenschaft einen so genannten Internetgateway automatisch einzurichten und somit ab und zu (vielleicht sogar öfters) Probleme zu verursachen. 

Verursacht wird das meist durch das Verwenden eines Routers der UPnP verwendet. Windows versucht dann die Konfiguration zum Router und Internet automatisch zu konfigurieren. Was beim Nutzen von mehreren Routern mit verschiedenen Einstellungen ja Sinn machen würde. Jedoch funktioniert das ganze nicht so wie es sollte und meist stirbt dadurch die Internetverbindung oder wird einfach verdammt langsam. Vorallem wenn Windows XP meint dies bei einem Router anwenden zu müssen, der eigentlich kein UPnP unterstützt ;) 

Entfernen dieses Internetgateway
*   Systemsteuerung
*   Software / "Windows-Komponenten hinzufügen/entfernen"
*   Netzwerkdienste
*   entfernen des Hakens bei "Internetgateway / Automatische Gatewaysuche" (oder so Ähnlich ;) )
*   Übernehmen
*   OK