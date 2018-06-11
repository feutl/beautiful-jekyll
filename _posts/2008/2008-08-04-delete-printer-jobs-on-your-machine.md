---
layout: post
title: Delete printer jobs on your machine
date: 2008-08-04
tags: [english, technology]
---

Script to stop/start and delete all printer jobs on a Windows machine
```cmd
@echo off

echo ### stop printer service ###
NET STOP SPOOLER
echo.

echo ### delete all files in printer spooler directory ###
rem (has to be adapted)
del /F /Q “C:\WINDOWS\system32\spool\PRINTERS\*.*”
echo.

echo ### start printer service ###
NET START SPOOLER
echo.

pause
```
