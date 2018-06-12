---
layout: post
title: MD5 / SHA1 Hashes erzeugen mit JAVA
date: 2006-01-26
tags: [deutsch, technology]
permalink: /md5-sha1-hashes-erzeugen-mit-java/
---

Während [Florian](http://blog.no-panic.at) und ich an unserem Projekt gearbeitet haben, welches in Kürze das Licht der großen WWWelt erblicken wird (also freut euch schon mal), musste ein Lösung her um MD5 bzw. SHA1 Hashes mit Java zu erzeugen. In PHP wie auch im .NET Framework funktionert das mehr oder weniger sehr einfach. Java ist da doch etwas anders und nach einiger Zeit im Netz suchend, habe ich dann doch die nötigen Infos gefunden um die folgende Klasse zusammenzubaun.

Die Klasse übernimmt einen String und liefert den MD5 / SHA1 Hash als String zurück:

```java
// erzeugen eines MD5 Hashes aus einem String
private String getMD5Hash(String password)
{
    String plainText = password;
    MessageDigest mdAlgorithm;  
    StringBuffer hexString = new StringBuffer();
    try
    {
        mdAlgorithm = MessageDigest.getInstance("MD5");
        mdAlgorithm.update(plainText.getBytes());
        byte[] digest = mdAlgorithm.digest();
        
        for (int i = 0; i < digest.length; i++)
        {
            plainText = Integer.toHexString(0xFF & digest[i]);
            
            if (plainText.length() < 2)
            {
                plainText = "0" + plainText;     
            }

        hexString.append(plainText);
        }
    }
    catch (NoSuchAlgorithmException ex)
    {
        ex.printStackTrace();
    }

    return hexString.toString();
}
```

Diesen Code konnte ich nicht Testen, aber ein informativer Blogleser hat ihn in den Kommentaren hinterlassen, darum möchte ich ihn euch in einer netten und brauchbaren Form präsentieren.

```java
public static String getMD5Hash(String in)
{
    StringBuffer result = new StringBuffer(32);        
    try
    {
        MessageDigest md5 = MessageDigest.getInstance("MD5");
        md5.update(in.getBytes());
        Formatter f = new Formatter(result);
        for (byte b : md5.digest())
        {
            f.format("%02x", b);
        }
    }
    catch (NoSuchAlgorithmException ex)
    {
        ex.printStackTrace();
    }
    
    return result.toString();
}
```
