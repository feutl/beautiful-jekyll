---
layout: post
title: Javascript und AJAX Debugging leicht gemacht
date: 2006-09-15
tags: [deutsch, technology]
---

Für alle die sich auf Grund des anhaltenden Hypes mit AJAX bzw. demzufolge auch mehr mit JavaScript beschäftigen stellt sich immer wieder die Frage wie man hier am einfachsten debuggen kann.

Wer Safari für das Testen seiner Websites verwendet hat es etwas schwerer als Firefox-User, aber auch hier gibt es eine Möglichkeit wie uns der [Apple Safari Develober FAQ](http://developer.apple.com/internet/safari/faq.html#anchor14) verspricht.

Safari enthält ein eigenes "Debug" Menu welches man jedoch zu allererst mittels `defaults write com.apple.Safari IncludeDebugMenu 1` einschalten muss. Danach erlaubt einem Safari verschieden Infos mittels Javascript in ein Debug Window zu schreiben. Der Befehl um während der Lauftzeit in das Debug Window schreiben zu können lautet: `window.console.log("I think therefore I code!");` Einfach an eine Stelle im JavaScript Code diese oder ähnliche Zeilen einfügen und beim Ausführen wird dann "hoffentlich" die Information dort stehen ;)

Leichter geht das ganze mit Firefox und der [Tamper Data Extension](https://addons.mozilla.org/firefox/966/) die noch viel mehr kann. Diese fängt den Traffic aller Requests und Responses zwischen Client und Server ab. Somit kann man angefangen vom Header bis hin über den gesendeten Body alles auslesen. Was es natürlich erleichtert AJAX Calls zu debuggen.

Weiters kann man POST, GET Variablen, Headers und und und während des Absenden ändern.