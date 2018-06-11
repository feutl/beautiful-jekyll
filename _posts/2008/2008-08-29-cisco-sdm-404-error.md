---
layout: post
title: Cisco SDM 404 Error
date: 2008-08-29
tags: [english, technology]
---

Ciscos SDM is sometimes used for configuring more complex router functions, after upgrading the SDM you could get a 404 error fot the path `https://IP_ADDRESSE/home/html/home_aux.shtml`

The reason for that is case sensitivity – that means that all Files on the Flash storage of your router have to be in lower case letters if not, SDM is not able to get loaded properly. The easiest way to change the wording of the files is using the rename command:

```
rename flash:COMMON.TAR common.tar
rename flash:ES.TAR es.tar
rename flash:HOME.TAR home.tar
rename flash:SDM.TAR sdm.tar
```
