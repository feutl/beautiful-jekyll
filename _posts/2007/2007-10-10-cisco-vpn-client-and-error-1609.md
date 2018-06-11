---
layout: post
title: Cisco VPN Client and Error 1609
date: 2007-10-10
tags: [deutsch, technology]
---

Wer mit dem Error 1609 bei der Installation des Cisco VPN Clients auf einem Windows System konfrontiert wird, dem kann unter Umständen geholfen werden. Dieser Fehler taucht auf, weil der VPN Client in seiner englischen Version einige Usergruppen auf deutschen Windows Installationen vermisst. Sozusagen ein Problem der Sprachen.

Gelöst wird das ganze mittels der Eingabe folgender Befehle in der Command Line (cmd) von Windows:

```
net localgroup Users /add
net localgroup Interactive /add
```

Voraussetzung dafür, Administratorrechte und schon sollte die Installation kein Problem mehr darstellen.