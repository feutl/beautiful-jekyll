---
layout: post
title: PPTP Einwahl für ÖJAB Heim unter Debian & Ubuntu
date: 2006-02-22
tags: [deutsch, technology]
---

Viele Leute verwenden für die Interneteinwahl in ÖJAB Heimen ein Tool genannt [PPTP Client](http://pptpclient.sourceforge.net/), ein ziemlich nettes Tool, doch wie installiert man dieses wenn es nicht auf der Installations-CD mitgeliefert wurde. Naja man fügt ein Repository hinzu und lässt "apt-get" oder "aptitude" die Arbeit machen - doch ohne INTERNET ????

Mein Lösung bis dato war immer mir einen Router zu besorgen der die Einwahl übernimmt - doch auf Dauer nervt das und so hab ich mich hingesetzt und versucht das ganze mittels den auf der CD angebotenen Mitteln zu lösen und es war bei weitem einfacher als gedacht.

Darum will ich hier ein kleines HowTo auf Deutsch schreiben:

1. `aptitude install pptp-linux`
2. `cp /etc/ppp/options.pptp /etc/ppp/options.pptp.bak`
3. `/etc/ppp/options.pptp` durch folgende Zeilen ersetzen
```
# Lock the port
lock
# Authentication
# We don't need the tunnel server to authenticate itself noauth
# We won't do EAP, CHAP, or MSCHAP, but we will accept MSCHAP-V2
# refuse-chap
# refuse-mschap
refuse-eap
# Compression
# Turn off compression protocols we know won't be used
nobsdcomp
nodeflate
```
4. `cp /etc/ppp/chap-secrets /etc/ppp/chap-secrets.bak`
5. `/etc/ppp/chap-secrets` durch folgende Zeilen ergänzen, hier muss man aber `username` gegen seinen VPN Login Namen ersetzen und `password` gegen das dazugehörige Passwort
```
# Secrets for authentication using CHAP
# client server secret IP addresses
username PPTP password *
```
6. `/etc/ppp/peers/heim` diese Datei mit folgendem Inhalt erstellen. die IP Adresse 172.16.0.1 kann sich unter Umständen ändern von Heim zu Heim - diese stellt nämlich die IP Adresse des PPTP Servers dar. Wiederum wie oben muss hier _username_ gegen den Login Namen ausgetauscht werden.
```
pty "pptp 172.16.0.1 --nolaunchpppd"
name username
remotename PPTP
require-mppe-128
file /etc/ppp/options.pptp
persist
ipparam heim
```
7. Jetzt müssen die RoutingTables gesetzt werden damit auch der komplette Traffic an den PPTP Server geschickt wird. Dies sollte keine Nachteile haben - nicht in Geschwindigkeit noch im Bezug auf das Transfervolumen. In diesem Sinne werden die Inhalte folgender Dateien ersetzt durch:
8. `/etc/ppp/ip-up` Die Inhalte dieses Files dienen dazu die RoutingTables beim Start der PPTP richtig zu setzen. Hier gilt es wieder das für PRIMARY sich die Werte ändern können wenn mehrer Netzwerkkarten vorhanden sind. Dies lässt sich mit ifconfig herausfinden und man trägt jenes Interface ein welches mit dem LAN es Heimes verbunden ist. Auch die IP Adresse des SERVERs könnte sich ändern - da schaut man aber einfach bei einem Windows Rechner nacht nachdem er sich eingewühlt hat oder fragt seinen Nachbar ;)
```bash
#!/bin/sh
# pppd ip-up script for all-to-tunnel routing
# name of primary network interface (before tunnel)
PRIMARY=eth0
# address of tunnel server
SERVER=192.168.10.1
# provided by pppd: string to identify connection aka ipparam option
CONNECTION=$6
if [ "${CONNECTION}" = "" ];
then CONNECTION=${PPP_IPPARAM};
fi
# provided by pppd: interface name
TUNNEL=$1
if [ "${TUNNEL}" = "" ];
then TUNNEL=${PPP_IFACE};
fi
# if we are being called as part of the tunnel startup
if [ "${CONNECTION}" = "heim" ];
then
    # direct tunnelled packets to the tunnel server
    route add -host ${SERVER} dev ${PRIMARY} 
    # direct all other packets into the tunnel
    route del default ${PRIMARY} route add default dev ${TUNNEL}
fi
```
9. `/etc/ppp/ip-down` Mittels dieses Files werden dir RoutingTables nach dem Beenden der PPTP wieder zurückgesetzt. Das PRIMARY Interfaces sollte das selbige wie bei Punkt 8 sein ;)
```bash
#!/bin/sh
# pppd ip-down script for all-to-tunnel routing
# name of primary network interface (before tunnel)
PRIMARY=eth0
# provided by pppd: string to identify connection aka ipparam option
CONNECTION=$6
if [ "${CONNECTION}" = "" ];
then CONNECTION=${PPP_IPPARAM};
fi
# provided by pppd: interface name
TUNNEL=$1
if [ "${TUNNEL}" = "" ];
then TUNNEL=${PPP_IFACE};
fi
# if we are being called as part of the tunnel shutdown
if [ "${CONNECTION}" = "heim" ] ;
then
    # direct packets back to the original interface
    route del default ${TUNNEL}
    route add default dev ${PRIMARY}
fi
```
10. Nun sollte alles fertig sein und mittels `pon heim` kann man die PPTP starten und `poff heim` beenden.
11. Wer nun die PPTP Einwahl automatisch beim Systemstart durchführen will trägt folgendes in die `/etc/network/interfaces` ein
```
# PPTP Einwahl automatisch
auto tunnel iface
tunnel inet ppp
provider heim
```

Nun sollte alles soweit klappen, bei Fragen einfach hier als Kommentar oder an mich persönlich. Weiters besteht noch die Möglichkeit weiterführende Informationen über [http://pptpclient.sourceforge.net/howto-ubuntu.phtml](http://pptpclient.sourceforge.net/howto-ubuntu.phtml) zu erhalten.