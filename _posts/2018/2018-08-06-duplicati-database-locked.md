---
layout: post
title: Duplicati - The database file is locked
date: 2018-06-08
tags: [english, technology]
published: false
---

After being unable to _Stop after Upload_ a backup job in [Duplicati](https://www.duplicati.om) on a QNAP, forcing the job to _Stop_ was necessary. This locked the database and restarting the backup job was impossible. This was the resulting error message:
> The database file is locked

The [Duplicati Forum](https://forum.duplicati.com/t/the-database-file-is-locked-after-stopping-backup-job/3761) was the last resort for help.

## Solution
1. Export the backup job as a file or to command line
2. Search for the `dpath` entry
3. Use `lsof` to find the processes locking the database
`lsof "/share/CACHEDEV1_DATA/.qpkg/Duplicati/.config/Duplicati/PJISXRFXEA.sqlite`
    * The output shows you the process and the process IDs, which can be used to restart or kill the service
    ```
    COMMAND     PID  USER   FD   TYPE DEVICE  SIZE/OFF      NODE NAME
    mono-sgen 23142 admin   22ur  REG  252,0 425369600 110105363 PJISXRFXEA.sqlite
    mono-sgen 23142 admin   24ur  REG  252,0 425369600 110105363 PJISXRFXEA.sqlite
    mono-sgen 23142 admin   29ur  REG  252,0 425369600 110105363 PJISXRFXEA.sqlite
    ```
6. Restart the services locking the database
5. Rerun the backup job
7. :+1:


## Links
* [The database file is locked after stopping backup job](https://forum.duplicati.com/t/the-database-file-is-locked-after-stopping-backup-job/3761?u=herbert)
* [Duplicati](https://www.duplicati.om)