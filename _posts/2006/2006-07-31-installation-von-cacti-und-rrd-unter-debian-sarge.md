---
layout: post
title: Installation von Cacti & RRD unter Debian Sarge [Single Server]
date: 2006-07-31
tags: [deutsch, technology]
---

Entschieden hab ich mich für Cacti, RRD und SNMP. SNMP ist auch lokal sehr brauchbar um Dienste, Services und andere Parameter abzufragen. Das ganze hab ich direkt aus dem Debian Source installiert - zwar bekommt man hier nicht die neueste Version und man kann auch nicht ganz so einfach verschieden Patches einspielen, aber mir war wichtig das ich ein stabiles System habe. Weiters sollten auch alle Abhängigkeiten aufgelöst werden und was am wichtigsten war - Updates sollen automatisch eingespielt werden, man verliert ja zu schnell den Überblick.

Nach vielen Howtos und Dokus ging es dann los:

## Zuerst den SNMP Dienst installieren

`aptitude install snmpd`

## SNMP konfigurieren

`nano /etc/snmp/snmpd.conf`

folgende Änderungen sind durchzuführen damit SNMP nur auf unseren localhost gebunden ist, auch nur diesen "ausspioniert" und von außen nicht verfügbar ist.
Im Abschnitt _Access Control_ stellen wir den "sec.name" auf "readonly" und die source wird auf localhost gebunden.

`com2sec readonly 127.0.0.0/24 public`

Den Abschnitt _System sontact information_ ändern wir einfach zu unserem Server passend ab:

```
syslocation Serverstandort
syscontact Root <root@localhost>
```

Am Ende der Datei fügen wir noch folgend Zeile ein, dies ist für einen lokalen Betrieb des SNMP Daemon nötig.
 
`smuxsocket 127.0.0.1`
 
## SNMP Daemon konfigurieren
Jetzt nur noch den snmpd direkt konfiguriert - es soll ja wirklich sichergestellt sein das dieser nur lokal horcht:
 
`nano /etc/default/snmpd`
 
Die Zeile SNMPDOPTS auskommentieren und / oder ersetzen durch `SNMPDOPTS='udp:127.0.0.1:161 -Lsd -Lf /dev/null -p /var/run/snmpd.pid'` Danach den snmpd restarten mit `/etc/init.d/snmpd restart`

So nun noch schnell testen ob alles klappt - Fehlermeldungen nicht ignorieren sondern ihnen auf den Grund gehen - schließlich kann ein offener SNMP einiges über den lokalen Rechner ausplaudern ;)
 
`snmpwalk -v 2c -c public localhost system`
 
## Einrichten der Cacti Datenbank
Zu empfehlen wäre, die Datenbank für Cacti und den nötigen User zu allererst anzulegen. Wichtig ist das der Cacti User für die MySQL Datenbank mind. PROCESS Rechte besitzt.
```sql
CREATE DATABASE cactidatabase;
GRANT PROCESS ON *.* TO 'cactiuser'@'localhost' IDENTIFIED BY 'Password';
GRANT SELECT , INSERT , UPDATE , DELETE , CREATE , DROP , INDEX , ALTER ON `cactidatabase` . * TO 'cactiuser'@'localhost';
FLUSH PRIVILEGES;
```

## Installation von Cacti

`aptitude install cacti cacti-cactid`

Die Fragen einfach mit den Default Antworten bestätigen, wenn man nicht genau weiß was nun sinnvoll ist, den Rest, wie sollte es anders sein, RICHTIG beantworten ;) Danach muss nur noch die Datenbank eingespielt werden `zcat /usr/share/doc/cacti/cacti.sql.gz | mysql -u cactiuser -p cactidatabase`

Das wars, Cacti sollte nun erreichbar sein unter http://meineDomain/cacti, vielleicht macht es noch Sinn ein paar Anpassungen auf der Security Seite zu treffen. Schließlich kann Cacti auch sehr brisante Informationen monitoren und somit preis geben und weiters führt Cacti PHP, Perl und Shell Scripts in regelmäßigen Abständen aus - und da könnten verschieden dunkle Gestalten schon auch auf blöde Ideen kommen.

Und ich bin der Meinung - Servermonitoring ist in diesem Ausmaß Admin Sache. Unterstützt haben mich bei dem Installieren von Cacti folgende Sites:
* [Cacti mit SNMP unter Debian](http://www.sspace.de/archives/3-Cacti-mit-SNMP-unter-Debian.html) 
* [The Cacti Manual](http://www.cacti.net/downloads/docs/html/)
* [CactiUsers: Documentation Site](http://cactiusers.org/wiki/Homepage)