---
layout: post
title: Some settings are managed by your organization
date: 2016-04-30
tags: [deutsch, technology]
---

Unter Windows 10 wollte ich ein paar Settings anpassen, konnte ich aber nicht da folgende Meldung "Some settings are managed by your organization" mich davon abhielt. Ganz konnte ich es jedoch nicht verstehen, schließlich bin ich auf meinem privaten Rechner meine eigene Organization oder? Administrator bin ich auch, also woher kam dieser Schwachsinn nun?

Nach etwas Recherche fand ich das Problem, nämlich die deaktivierte "Telemetry" Einstellung erzeugt das verhalten. Man muss nicht verstehen warum das so ist oder? Schnell wieder eingeschalten und ich konnte auch wieder alle zuvor gesperrten Einstellungen anpassen.

Normalerweise ist die Einstellung auch nicht deaktiviert, aber sobald man bei Windows 10 einige Sicherheitseinstellungen anpasst kann das schon schnell passieren. Ich würde es auch jedem empfehlen dem gesprächigen Windows 10 dieses "nach-hause-telefonieren" einzuschränken. Am einfachsten geht es mit dem Tool [O&O ShutUp 10](https://www.oo-software.com/de/shutup10/update). 

## Steps to fix 'Some settings are managed by your organization' message in Windows 10

1. Launch Start Menu by hitting the Windows Key. Type in `gpedit.msc` and right-click the app from the search results. Choose `Run as Administrator` from the context menu.
2. In the Group Policy Editor (gpedit.msc), go `to Computer Configuration/Administrative Templates/Windows Components/Data Collection` and `Preview Builds.`
3. Find the `Allow Telemetry` item and double-click it to edit the policies.
4. Change the setting to `Enabled`. Change the drop-down menu entry to `3-Full` and click `Apply`.
5. Now open the item again and change its Setting to `Not configured` and hit the `Save`button.


## Quelle
* [http://www.ibtimes.co.uk/how-fix-some-settings-are-managed-by-your-organization-message-windows-10-1521281](http://www.ibtimes.co.uk/how-fix-some-settings-are-managed-by-your-organization-message-windows-10-1521281)