---
layout: post
title: Festplattenüberwachung unter Linux
date: 2006-07-23
tags: [deutsch, technology]
---

Nachdem unser Server mal wieder bissal Mukken macht bzw. gemacht hat (hoffentlich bleibt es so) musst mal nachgeguckt werden warum die Festplatte im Read-Only Mode waren.

Es war kein Dienst schuld und auch kein anderes Stück Software somit blieb nur mehr Hardware Probleme. Also musste ein Überwachungstool für die Festplatte her.

[SmartMon](http://smartmontools.sourceforge.net/) bzw. die [SmartMonTools](http://smartmontools.sourceforge.net/) mussten her - fürs erste ;) (jaja [Flo](http://blog.no-panic.at/) und [Hirschy](http://www.dont-panic.at/) da kommt noch mehr).

Ermöglicht wird das ganze durch die [Self-Monitoring, Analysis and Reporting Technology kurz S.M.A.R.T](http://en.wikipedia.org/wiki/Self-Monitoring%2C_Analysis%2C_and_Reporting_Technology). welche es der Festplatte erlaubt sich selbst zu überwachen.

Die SmartMonTools dienen nun nur mehr zum Auslesen dieser Informationen, Filtern und zum Anstoßen verschiedener Aufgaben wie SelfChecks in den verschiedensten Varianten oder auch Notifications über den aktuelen Health Status.

Wie das ganze nun eingerichtet wird ist schnell erklärt. über den PackageManager der Distribution installieren oder selber basteln. Den Deamon starten damit hier dauerhaft überwacht wird - dazu gibt es ein gut erklärtes Config File smartd.conf.

Ja und wer mal zwischendurch nachgucken will was so läuft - der nutzt einfach das 2te Tool smartctl um mittels verschiedener Parameter die S.M.A.R.T. Infos abzufragen. Ja und ein paar gute Seiten habe ich auch gefunden, welche die SmartMonTools näher erklären und mir beim Einrichten sehr behilflich waren

* [S.M.A.R.T. Festplattendiagnose einrichten](http://www.linux-fuer-alle.de/doc_show.php?docid=240&catid=10)
* [Linux Harddisk Monitoring with SmartMonTools (smartctl)](http://www.captain.at/howto-linux-smartmontools-smartctl.php)
* [Monitoring Hard Disks with SMART](http://www.linuxjournal.com/article/6983)