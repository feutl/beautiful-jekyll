---
layout: post
title: Windows 10 Storage Spaces und WD Green Drives
date: 2016-04-17
image: /img/2016/wd-green-drives-thumb.jpg
bigimg: /img/2016/wd-green-drives.jpg
tags: [deutsch, technology]
---

Bei mir zu Hause läuft Windows 10 als NAS Lösung auf meinem [HP N40L Microserver](http://n40l.wikia.com/wiki/HP_MicroServer_N40L_Wiki). Als Platten hab ich [3TB WD Green](http://www.wdc.com/) Drives verbaut. Im nachhinein war das keine gute Wahl, aber jetzt muss damit gelebt werden.

Mit Linux basierenden NAS Lösungen wie [RockStor](http://rockstor.com/) waren die Platten auch ohne Probleme verwendbar. Doch da es Green Disks sind musste zuerst mit WDIDLE3 eingegriffen werden um das "Excessive Head Parking" los zu werden. Wenn das nicht gemacht wird, erhöhen sich der S.M.A.R.T Wert für "load cycles" innerhalb von einem Tag um 500 bis 600 Einheiten, was die Platte ziemlich schnell in den Tod jagt.

Mit [Microsofts Storage Spaces](https://technet.microsoft.com/en-us/library/hh831739.aspx) kommt noch ein weiteres Problem dazu. Da Green Disks sehr langsam "aufwachen" werden die Platten gerne von Microsofts Storage Spaces "retired". Damit sind sie nicht mehr Teil des Storage Pools und werden durch eine Spare Disk ersetzt bzw. die Daten der retired Disk auf die vorhanden Platten verteilt. Das ist meist weiter nicht tragisch, der Storage Pool ist damit nicht optimal genutzt aber je nach RAID Lösung weiter funktional. Wir wissen nun zwar das die Platte keine Probleme macht und alles in Ordnung ist, ihr einziges Problem ist eine Green Disk zu sein ;) Unser Problem ist jedoch, dass MS keine Möglichkeit bietet über die GUI die Platte wieder online zu bringen oder dieses Verhalten zu verändern. Doch PowerShell hilft aus.

## WDIDLE3
Am einfachsten bekommt man WDIDLE3 mittels [Ultimate Boot CD](http://www.ultimatebootcd.com/) danach kann man mit _wdidle3.exe_ den Status verifizieren und mit _wdidle3.exe /D_ den IDLE Mode der Platte deaktivieren. Von da an übernimmt das Betriebssystem die Aufgabe wieder.

[How to Stop Excessive Load Cycles on the Western Digital 2TB Caviar Green (WD20EARS) with WDIDLE3](http://www.storagereview.com/how_to_stop_excessive_load_cycles_on_the_western_digital_2tb_caviar_green_wd20ears_with_wdidle3)

## MS Storage Spaces
Um Microsofts Storage Spaces etwas nachzuhelfen kann man das Verhalten eines Storages Spaces anpassen, speziell jenes wenn Microsoft nicht genau weiß was es mit einer Disk anstellen soll die eigenartig reagiert bzw. gerade nicht verfügbar ist.

```powershell
Set-StoragePool -FriendlyName "Storage pool" -RetireMissingPhysicalDisks Never
```

> [Technet Set-StoragePool](https://technet.microsoft.com/en-us/library/hh848672(v=wps.630).aspx) RetireMissingPhysical Specifies when Windows should set the Usage property of physical disks missing from a storage pool to Retired.

Sollten Platten doch den "retired" Status erhalten hilft folgender Befehl um sie wieder online zu bringen.
```powershell
Set-PhysicalDisk -FriendlyName "Diskname" -Usage AutoSelect
```