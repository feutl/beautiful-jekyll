---
layout: post
title: Configure Austrians Daylight Saving Time on Cisco Devices
date: 2008-03-31
tags: [deutsch, technology]
---

Die Sommerzeit hat wieder zugeschlagen und jeder vergisst gerne mal darauf seine Uhr früh genug umzustellen. Wie schön wäre es, wenn das automatisch geschieht. Aus diesem Grund werden auch immer mehr und mehr Devices automatisch mit einem Zeitserver synchronisiert. Sehr bekannt in der IT Landschaft ist die Nutzung des [NTP (Network Time Protocol)](http://de.wikipedia.org/wiki/Network_Time_Protocol). So auch bei Cisco Devices, leider vermisst man bei den amerikanischen Produkten der Firma Cisco oft die nötigen Voreinstellungen um neben NTP auch die Sommer- und Winterzeit Umstellung automatisch geschehen zu lassen. Hierzu wurden vor Jahren [Regeln für die einzelnen Zeitzonen](http://de.wikipedia.org/wiki/Sommerzeit#Letzte_und_n.C3.A4chste_Umstellungen) definiert, Cisco Devices kennen jedoch die europäischen Regeln dafür meist nicht. Abhilfe schaffen folgende zwei Kommandes die einerseits die Zeitzone des Devices richtig setzt und andererseits die Regel für Sommer-Winter-Zeit-Umschaltung (Folgende Regelung gilt in den Ländern der Europäischen Union, auch in der Schweiz, im EWR (außer Island) und einigen anderen Ländern).

```
clock timezone UTC/GMT 1
clock summer-time CEST recurring last Sun Mar 2:00 last Sun Oct 2:00
```

Und wär im gleichen Zuge auch gleich NTP auf seinem Cisco Device aktivieren möchte kann das mit:

```
ntp server 129.6.15.28
```

Der oben genannt Server ist ein offizieller [NIST Server](http://tf.nist.gov/service/time-servers.html) und wer solchen nicht verwenden möchte hat auf [pool.ntp.org](http://www.pool.ntp.org/) eine Auswahl und ausgezeichnete Anlaufstelle. Verifizieren kann man die Einstellung und Funktion mit:

```
CiscoR# sh clock detail
13:08:09.880 UTC/GMT Fri Mar 28 2008
Time source is NTP
Summer time starts 02:00:00 UTC/GMT Sun Mar 30 2008
Summer time ends 02:00:00 CEST Sun Oct 26 2008
```

Weiter Links zu NTP auf Cisco Devices
*   [Synchronize a Cisco router's clock with Network Time Protocol (NTP)](http://articles.techrepublic.com.com/5100-10878_11-5712046.html)
*   [Configuring Cisco devices to use a ClockWatch NTP Server](http://www.beaglesoft.com/clwaciscontp.htm)
*   [Basic System Management](http://www.cisco.com/en/US/docs/ios/12_2/configfun/configuration/guide/fcf012_ps1835_TSD_Products_Configuration_Guide_Chapter.html#wp1001170)