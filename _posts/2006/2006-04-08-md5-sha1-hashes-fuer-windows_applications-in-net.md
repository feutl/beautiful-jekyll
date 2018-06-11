---
layout: post
title: MD5 / SHA1 Hashes für WindowsApplications in .NET
date: 2006-04-28
tags: [deutsch, technology]
---

Für Windows Applications mittels .NET ist es bei weitem nicht so einfach einen MD5 / SHA1 Hash zu erzeugen wie für ASP.NET Projects. Nach ein bißchen Zeit, lesen und probieren hab ichs dann doch geschafft und hier gibts die Function:

## VB.NET

```VB.net
Private Function MyMD5Hasher(ByVal text As String) As String
 	Dim strHash As String = ""
   	Dim md As MD5 = MD5CryptoServiceProvider.Create()
   	Dim hash() As Byte
   	Dim enc As ASCIIEncoding = New ASCIIEncoding()
   	Dim buffer() As Byte = enc.GetBytes(text)
   	Dim b As Byte

   	hash = md.ComputeHash(buffer)
   	For Each b In hash
   		strHash += b.ToString("x2")
   	Next

   	Return strHash
End Function
```

## C\#

```C#
private string MyMD5Hasher(string text)
{
   	string strHash = "";
   	MD5 md = MD5CryptoServiceProvider.Create();
   	byte[] hash;
   	ASCIIEncoding enc = new ASCIIEncoding();
   	byte[] buffer = enc.GetBytes(text);
   	byte b;

   	hash = md.ComputeHash(buffer);
   	foreach (int b in hash)
    {
   		strHash += b.ToString("x2");
   	}
    
    return strHash;
}
```

Wer MD5 / SHA1 Hashes mit Java erzeugen will findet auch in meinem Blog die Antwort [test](2006-01-26-md5-sha1-hashes-erzeugen-mit-java.md)