---
layout: post
title: Permissions mixed up on QNAP
date: 2011-11-24
tags: [deutsch, technology]
permalink: /permissions-mixed-up-on-qnap/
---
Working with AFP/SMB on your QNAP and different users and/or operating systems can mess up your file permissions. The reason therefore is pretty complicated - but the solution to fix it is much easier.

So if you ever tried to delete a file and it was not possible, or a file was hidden instead of normal viewable - but all of that should work - this trick could help you.
Login to your QNAP using SSH and use

```
set_volume_mode _name_of_share_
ex.: set_volume_mode Qmultimedia
```

All problems solved, permissions on the file system itself are corrected and you can go on with your work :)