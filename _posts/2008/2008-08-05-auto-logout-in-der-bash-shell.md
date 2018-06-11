---
layout: post
title: Auto-Logout in der Bash Shell
date: 2008-08-05
tags: [deutsch, technology]
---

Eingelogged ist man oft schneller als ausgelogged. Sehr problematisch ist es, wenn eine Root-Shell nach dem Verlassen des Computers offen bleibt und jeder Anwesende hier herumwerken kann. Aus diesem Grund gibt es innerhalb der Bash Shell die Environment Variable TMOUT, setzt man diese, entweder per Hand mit `export TMOUT=120` oder innerhalb der .bashrc oder `/etc/profile`, wird ein automatisches Logout nach der angegebenen IDLE Time durchgeführt.

Ich hab folgendes in meiner `/etc/profile` stehen:
```bash
IDLELOGOUT=120
echo “Automatischer Logout nach $IDLELOGOUT sekunden!”
export TMOUT=$IDLELOGOUT
```

Damit werden alle User automatisch nach der bestimmten Inaktivität ausgelogged. Bitte nicht vergessen, wer als User eingelogged ist und mittels `sudo su` die Root-Recht erlangt hat wird nicht automatisch ausgelogged. Um dieses Problem zu lösen muss ich noch etwas nachforschen.