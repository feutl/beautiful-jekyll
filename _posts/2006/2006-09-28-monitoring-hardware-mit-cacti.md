---
layout: post
title: Monitoring Hardware mit Cacti
date: 2006-09-28
tags: [deutsch, technology]
---

Wäre es nicht nett, wenn man die Temperatur seiner Festplatte(n), seines Motherboards, seiner CPU und die Umdrehungsgeschw. seiner Lüfter im Auge behalten kann?

Noch schöner wäre das ganze auch noch mit Cacti in Kombination. Nach langem suchen hab ich vor Monaten einige nettes Scripts auf [wlug](http://www.wlug.org.nz/TitleSearch?s=cacti) gefunden. Vorweg möchte ich noch sagen bevor ich näher Beschreibe wie ich vorgegangen bin, dass alle Versuche das Monitoring über SNMP an dem nötigen wissen von SNMP (so glaube ich) gescheitert sind.

Also ab zur Vorbereitung, denn was zu aller erst am Server vorhanden sein muss ist _lm-sensors_ und _hddtemp_. Zwei verdammt nette Tools mit welchen ich glaub ich noch einige schöne Dinge zaubern könnte ;)

Eine Installationsanleitung dieser Tools findet man auf [Debian Administrator :: Monitoring your hardware's temperature](http://www.debian-administration.org/articles/327). 

Weiters brauchen wir noch ein paar Scripts die uns ermöglicht über die oben genannten Tools die Daten auszulesen und sie für Cacti zur Verfügung zu stellen.

## HDD Temperatur
Bei diesem Script musst ich ein paar kleinere Änderungen durchführen damit es auch sauber mit dem Cacti Daemon läuft und nicht immer mit Fehlermeldungen frühzeitig beendet wird.
### hdtemp.php
`#!/usr/local/bin/php -f`

Zu diesem Script gibt es nicht viel zu erklären, einzig und allein wichtig dafür ist, dass man _smartctl_ mittels _sudo_ ausführen kann und der Cacti Daemon auch die nötigen rechte dazu hat. Grund dafür ist, da _smartctl_ auf Hardware nahe Daten zugreift ist es natürlich klar das nur _root_ das darf ;)

## Motherboard / CPU Temperatur & Fan Speeds
### check_sensors.pl
``` perl
#!/usr/bin/perl
@sensoroutput=`/usr/bin/sensors`;
foreach(@sensoroutput) {
    chomp();
    split();
    if ( $_[0] eq 'MBTemp:' ) {
        $temp1 = $_[1];
    }
    if ( $_[0] eq 'CPUTemp:' ) {
        $temp2 = $_[1];
    }
    if ( $_[0] eq 'UknFan:' ) {
        $fan1 = $_[1];
    }
    if ( $_[0] eq 'CPUFan:' ){
        $fan2 = $_[1];
    } 
}

$temp1 =~ s/+//;
$temp1 =~ s/?C//;
$temp2 =~ s/+//;
$temp2 =~ s/?C//;
print "fan1:$fan1";
print " ";
print "fan2:$fan2";
print " ";
print "temp1:$temp1";
print " ";
print "temp2:$temp2";
```

Dieses Script benötigt etwas Vorbereitung. Da hier der Output von _sensors_ gefiltert wird und die richtigen Werte ausgelesen werden, ist es nötig für alle Fans und Temperatur-Sensoren ein _IF Statement_ anzulegen und den Namen des jeweiligen Datenlieferanten anzugeben.

Herausfinden tut man diesen am einfachsten indem man sich die Ausgabe des Befehls _sensors_ genau ansieht, sich dort die nötigen Namen sucht und diese einträgt.

Wer seine eigenen Namen festlegen will kann das über die _sensors.conf_ Datei. Dort sucht man einfach nach seinem Motherboardtyp (wird im Output von _sensors_ ganz oben angegeben) und editiert dann alles nach seinen Wünschen ([lm-sensors Homepage](http://www.lm-sensors.org/)).

Meine _sensors.conf_ sieht folgendermaßen aus:
```
label temp1 "MBTemp" #"M/B Temp"
label temp2 "CPUTemp" #"CPU Temp"
ignore temp3 
label fan1 "UknFan"
label fan2 "CPUFan" #"CPU Fan"
ignore fan3
```

Bitte ändert alle labels so, dass keine Leerzeichen vorhanden sind, ab und zu traten bei mir dadurch Probleme auf. Das wars im großen und ganzen, diese Dateien noch als "ausführbar" markieren und ins richtige Verzeichniss für den Cacti Daemon kopieren.