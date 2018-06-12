---
layout: post
title: Dynamisches DNS mit Duck DNS und Barracuda NextGen Firewall F
date: 2016-05-07
tags: [deutsch, technology, barracuda]
bigimg: /img/2016/duckdns-header.png
permalink: /dynamisches-dns-mit-duck-dns-und-barracuda-nextgen-firewall-f/
---

## Was ist DDNS?
> Dynamisches DNS oder DDNS ist eine Technik, um Domains im Domain Name System (DNS) dynamisch zu aktualisieren. Der Zweck ist, dass ein Computer (bspw. ein PC oder ein Router) nach dem Wechsel seiner IP-Adresse automatisch und schnell den dazugehörigen Domaineintrag ändert. So ist der Rechner immer unter demselben Domainnamen erreichbar, auch wenn die aktuelle IP-Adresse für den Nutzer unbekannt ist. [Wikipedia](https://de.wikipedia.org/wiki/Dynamisches_DNS)

Der populärste Vertreter ist sicherlich [Dyn.com](https://dyn.com/dns/) (früher auch DynDNS.org), jedoch gibt es das gratis Service schon länger nicht mehr. Darum gibt es auch viele freie Angebote die Versuchen den Platz einzunehmen, eines davon ist [Duck DNS](https://www.duckdns.org/). Es verspricht eine einfach Nutzung und hat IPv4 und IPv6 Support. Der unbezahlte Account kann bis zu 5 Domains mit IPs versehen und das über einen einfachen HTTPS Post. 

Damit war der Weg bereit für eine Implementierung von Duck DNS auf einer NextGent Firewall F von Barracuda und ich war überrascht wie einfach und schnell sie zu realisieren war.

## Schritt für Schritt Anleitung

1.  Auf [DuckDNS.org](http://duckdns.org) einen Account anlegen
2.  Domain hinzufügen
    ![duckdns add domain](/img/2016/duckdns-add-domain.png)
3.  Duck DNS Token notieren
4.  Per SSH auf die die NextGen Firewall verbinden
5.  Ein neues Verzeichnis anlegen mit `mkdir /root/duckdns/`
6.  Mittels `cd /root/duckdns/` ins das neue Verzeichnis wechseln
7.  Eine neue Datei anlegen `touch duck.sh`
8.  Mit einem Editor öffnen `nano duck.sh`
9.  Folgenden Inhalt einfügen, man kann ich nach folgenden Schema selbst zusammenstellen oder über den Menüpunkt Install > linux cron auf der Duck DNS Seite erzeugen lassen
    
    `echo url="https://www.duckdns.org/update?domains=[mydomain]&token=[myToken]&ip=" | curl -k -o ~/duckdns/duck.log -K -`
10.  Das Script ausführbar machen (und testen) `chmod 700 duck.sh`
    ![duckdns test script](/img/2016/duckdns-test-script.png)
11.  Damit das Script regelmäßig ausgeführt wird per NextGen Admin Configuration > Advanced Configuration > System Scheduler einen neuen Cron Job unter Daily / Intrahour einführen.
    ![duckdns nextgen admin schedule](/img/2016/duckdns-nextgen-admin-schedule.png)
12.  Ein Log File wird in das selbe Verzeichnis wie das Script geschrieben und die erfolgreiche Ausführung des Scripts findet man im System Log (Box > System > cron).
    [![duckdns nextgen admin log](/img/2016/duckdns-nextgen-admin-log.png)