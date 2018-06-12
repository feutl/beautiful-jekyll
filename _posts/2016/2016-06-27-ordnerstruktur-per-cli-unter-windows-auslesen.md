---
layout: post
title: Ordnerstruktur per CLI unter Windows auslesen
date: 2016-06-27
tags: [deutsch, technology]
---

Immer wieder benötigt man die Ordnerstruktur und die darin abgelegten Dateien als einfachen Text. Entweder um die Liste der Inhalte per eMail weiterzuleiten oder sie als einfachen Text abzuspeichern. Windows bietet einem mehrere Möglichkeiten dies zu erreichen.

## Tree Tool (cmd)

Aus der MS-Dos / Windows XP Ära kommt [_tree_](https://www.microsoft.com/resources/documentation/windows/xp/all/proddocs/en-us/tree.mspx?mfr=true) und man findet es auch auf den neueren Windows Systemen.

* `tree <pfad>` liefert die Ordner und Unterordner des gewählten Ordners
* `tree /f <pfad>` liefert neben den Ordnern und Unterordnern auch die Dateien innerhalb der Ordner
* `tree /a <pfad> oder tree /f /a <pfad>` liefert das Ergebnis mit reinen ASCII Zeichen

![Directory Listing CMD tree](/img/2016/directory-listing-cmd-tree.png)]
Seit Windows Vista gibt es auch die Möglichkeit den Inhalt direkt in die Zwischenablage kopieren zu lassen.

`tree <path> | clip`

## Get-ChildItem (powershell)

Wär auf moderne Art und Weise die Ordnerstruktur textuell darstellen möchte kann sich auch mit PowerShell behelfen. Viel flexibler und mit mehr Darstellungsmöglichkeiten versehen, dass beschreibt auch [Microsofts Scripting Guy](https://blogs.technet.microsoft.com/heyscriptingguy/2014/02/03/list-files-in-folders-and-subfolders-with-powershell/).

* `Get-ChildItem -Path <path> | tree` liefert die Ordner und Unterordner des gewählten Ordners
* `Get-ChildItem -Path <path> -File - Recurse` liefert alle Ordner, Unterordner und Files. Jedoch geht erzeugt hier die Kombination mit _tree_ nicht zum selben Ergebnis wie _tree (cli)_

![Direcotry Listing PowerShell](/img/2016/direcotry-listing-powershell.png)]
Die Flexibilität von [_Get-ChildItem_](https://technet.microsoft.com/en-us/library/hh849800.aspx) erlaubt auch den Export in CSV, XML und Datenbanken.

`Get-ChildItem -Recurse <path> *.xml | Select-Object -Property FullName,name | Export-Csv directory_structure.csv`

## DIR (cli)

* `dir <path> /S` liefert alle Ordner, Unterordner und Files. Die Ausgabe ist ähnlich zu `Get-ChildItem -Path <path> -File - Recurse`
* `dir <path> /S /B` liefert alle Ordner, Unterordner und Files mit voller Pfadangabe als einfache Liste

![Directory Listing CMD DIR](/img/2016/directory-listing-cmd-dir.png)]