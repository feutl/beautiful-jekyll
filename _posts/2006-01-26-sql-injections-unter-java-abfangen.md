---
layout: post
title: SQL Injections unter Java abfangen
date: 2006-01-26
tags: [deutsch, technology]
---

Das Projekt das [Florian](https://blog.no-panic.at/) und ich gerade in Arbeit haben zeigt uns immer wieder neue Möglichkeiten die uns Java und AJAX bieten. Es werden fast täglich neue Ideen geboren und hinzugefügt und wir freuen uns schon euch allen unsere Arbeit zeigen zu können.

Doch zuerst ein Hoch an Java welches es wie auch das .NET Framework schafft, SQL Injectinos selbst zu handlen, was mir persönlich einiges an Arbeit abnimmt bzw. erspart (nachdem ich den Replacer zuerst händisch geschrieben habe ;) ). Um euch diese Arbeit zu ersparen hier das Code Sample mit *PreparedStatement* welche fast genauso funktionieren wie normale *Statement Objekte*, jedoch einige Zusatzfeatures bieten.

```java

String query = "INSERT INTO tbl_feed (user_ID, feedurl, feedname) VALUE (? ,?, ?)";

PreparedStatement pstmt= conn.prepareStatement(query);
pstmt.setString(1, userID);
pstmt.setString(2, feeds[i][1]);
pstmt.setString(3, feeds[i][0]);

pstmt.executeUpdate();
```

Funktionsweise:

Man verwendet PreparedStatement genauso wie Statement mit einem großen Vorteil, man baut den Query String zusammen und alle dynamisch Werte werden mit einm *"?"* ersetzt.
Danach kann man jedes *"?"* mittels *setString(position, string)* ersetzen und das *PreparedStatement Objekt* handled das Escapen der nötigen Zeichen selbstständig.