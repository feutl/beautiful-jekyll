---
layout: post
title: Chatten auf Cisco Routern
date: 2008-04-24
tags: [deutsch, technology]
---

Auf Cisco Routern können sich mehrere User gleichzeitig einloggen. Die Konsole und Virtuelle Terminal Lines machen es möglich, doch wie schafft man es diesen angemeldeten Usern mitzuteilen das z.B. ein Router neu gestartet werden muss bzw. wie teilt man ihnen einfach und schnell etwas mit?

```
send *
```

Mit diesem Befehl kann man eine Nachricht an alle angemeldeten User schicken, doch vorsicht mit STRG + Z wird die Nachricht versendet.

```
send *
Enter message, end with CTRL/Z;
abort with CTRL/C:
The sky is falling, so I'm going to reload the router in 5 minutes.
It's been nice knowing you. ^Z
```

Und natürlich kann man auch bestimmten Usern Nachrichten schicken:
```
send 66
```

sendet dem User der Line 66 eine Nachricht - so wie
```
send console 0
```

dem User auf der Konsole eine Nachricht hinterlässt.