---
layout: post
title: Firehol Integration für die Barracuda CloudGen Firewall
date: 2019-02-02
tags: [deutsch, technology, barracuda]
bigimg: /img/2019/2019-02-02-firewall-history.png
---

[iplists.firehol.org](http://iplists.firehol.org/) stellt eine Liste von IP Adressen und Netzwerken zur Verfügung, die man als bösartig einstufen könnte. Heißt, Zugriffe von und auf diese IPs kann man getrost blockieren und schafft somit mehr Sicherheit für das eigene Netzwerk. Ganz speziell, wenn man Services (zB. eine [Nextcloud](https://nextcloud.com/)) selbst hosted.

[firehol.org](www.firehol.org)
> FireHOL is a language (and a program to run it) which builds secure, stateful firewalls from easy to understand, human-readable configurations. The configurations stay readable even for very complex setups.

[iplists.firehol.org](http://iplists.firehol.org/)
> This site analyses all available security IP Feeds, mainly related to on-line attacks, on-line service abuse, malwares, botnets, command and control servers and other cybercrime activities.

# Importieren der Level 1 IPLIST
Eine Integration mit der CloudGen Firewall ist nicht von Haus aus vorgesehen,daher habe ich mir das ganze selbst gestrickt. Mit folgenden Befehlen kann man eine Liste, in meinem Fall die Level 1 Liste, herunterladen und in ein Netzwerkobjekt importieren.

Ich habe die CustomExternalObjects gewählt da es hier egal ist ob es sich um eine IP Adresse oder ein Netzwerk in CIDR Notation handelt. Das Objekt verkraftet auch IPv4 und IPv6 Adressen gleichermaßen. Mehr dazu auf [campus.barracuda.com](https://campus.barracuda.com/doc/73719276/)

```bash
# ladet die aktuelle level 1 liste herunter uns speichert sich lokal
curl https://iplists.firehol.org/files/firehol_level1.netset --output /var/phion/home/firehol_level1.netset

# entfernt alle eingefügten kommentera, beginnend mit einem #
sed '/#/d' /var/phion/home/firehol_level1.netset > /var/phion/home/addresses.dirty

# ersetzt die Zeilenumbrüche durch Leerzeichen damit wir ein konformes File für den Import besitzen
tr '\n' ' ' < /var/phion/home/addresses.dirty > /var/phion/home/addresses

# importiert die Inhalte in das erste CustomExternalObject
/opt/phion/bin/CustomExternalAddrImport -i /var/phion/home/addresses -o 1
```

![befülltes Objekt](/img/2019/2019-02-02-customexternalobject-content.png)


# Regelmäßige Aktualisierung
Wichtig ist natürlich auch, die Informationen der Listen regelmäßg zu erneuern, damit neue IPs hinzugefügt, und alte gelöscht werden. Dafür habe ich die einzelnen Befehle in ein Shell Script verpackt, welches zur Kontrolle auch ein Log File schreibt. Diese Script kann über den internen Scheduler einmal täglich aufgerufen werden, vorausgesetzt `chmod +x` wurde nicht vergessen.

```bash
#!/bin/bash

dt=$(date '+%d/%m/%Y %H:%M:%S')
logfile="/root/firehol/firehol.log"

echo "$dt - Script Started" >> $logfile

echo "Fetching firehol_level1.netset" >> $logfile
curl https://iplists.firehol.org/files/firehol_level1.netset --output /var/phion/home/firehol_level1.netset

echo "Removing comments from file and write to addresses.dirty" >> $logfile
sed '/#/d' /var/phion/home/firehol_level1.netset > /var/phion/home/addresses.dirty

echo "Replace new line with space" >> $logfile
tr '\n' ' ' < /var/phion/home/addresses.dirty > /var/phion/home/addresses

echo "Import addresses to custom external object" >> $logfile
/opt/phion/bin/CustomExternalAddrImport -i /var/phion/home/addresses -o 1

echo "$dt - Script Stopped" >> $logfile
echo "---------------------------------------------"  >> $logfile

# logfiles to verify
# custom log $logfile path
# CustomExternalImport log file located at the firewall service log path
```

Im System Scheduler verweist man auf den Pfad des Scripts

```bash
/root/firehol/firehol.sh > /dev/null 2>&1 &
```

![System Scheduler Intraday Task](/img/2019/2019-02-02-system-scheduler.png)

# Access Rule

Dieses Objekt verbaut man dann einfach in eine Access Rule (Inbound oder / und Outbound) und hat sehr einfach die Sicherheit seiner Services und Umgebung erhöht.

![access rule](/img/2019/2019-02-02-access-rule.png)

Und so sieht, in meinem Fall, die Firewall History aus.

![Firewall History](/img/2019/2019-02-02-firewall-history.png)