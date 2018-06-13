---
layout: post
title: Duplicati - The database file is locked
date: 2018-06-13
tags: [english, technology]
image: /img/2018/duplicati.png
gh-repo: duplicati/duplicati
gh-badge: star
---

After being unable to _Stop after Upload_ a backup job in [Duplicati](https://www.duplicati.om) on a QNAP, forcing the job to _Stop_ was necessary. This locked the database and restarting the backup job was impossible. This was the resulting error message:

```
The database file is locked.
```

The [Duplicati Forum](https://forum.duplicati.com/t/the-database-file-is-locked-after-stopping-backup-job/3761) was the last resort for help.

## Resolve Locked Database
1. Export the backup job as a file or to command line
2. Search for the `dpath` entry
3. Use `lsof` to find the processes locking the database
    `lsof "/share/CACHEDEV1_DATA/.qpkg/Duplicati/.config/Duplicati/PJISXRFXEA.sqlite`
    
    * The output shows you the process and the process IDs, which can be used to restart or kill the service

    ```bash
    COMMAND     PID  USER   FD   TYPE DEVICE  SIZE/OFF      NODE NAME
    mono-sgen 23142 admin   22ur  REG  252,0 425369600 110105363 PJISXRFXEA.sqlite
    mono-sgen 23142 admin   24ur  REG  252,0 425369600 110105363 PJISXRFXEA.sqlite
    mono-sgen 23142 admin   29ur  REG  252,0 425369600 110105363 PJISXRFXEA.sqlite
    ```
6. Restart the services locking the database
5. Rerun the backup job
7. :+1:

Able to start the backup again, it ended with another error giving me a list of files stored on the remote location. The backup was not successful, repairing the database for the backup job was my next best guess - which resulted in another error.

```
2018-06-11 13:25:17 +02 - [Error-Duplicati.Library.Main.Operation.RepairHandler-CleanupMissingFileError]: Failed to perform cleanup for missing file: duplicati-b58bcb8fcefe141a2ba3a92aea3497758.dblock.zip.aes, message: Repair not possible, missing 582 blocks.
If you want to continue working with the database, you can use the "list-broken-files" and "purge-broken-files" commands to purge the missing data from the database and the remote storage.
```

The hint in the error message led me to the two additional comments I could use to work around the error and get the backup job running again.

## List and Purge Broken Files
1. Export the backup job to command line
2. Replace the `backup`command with `list-broken-files` and/or `purge-broken-files` respectively.
    * Command Line example on a QNAP
    `/opt/Qmono/bin/mono /share/CACHEDEV1_DATA/.qpkg/Duplicati/Duplicati/Duplicati.CommandLine.exe purge-broken-files "ssh://172.16.10.10:22//mnt/data/?auth-username=user&auth-password=user&ssh-fingerprint=ssh-rsa%" --backup-name=data --dbpath=/share/CACHEDEV1_DATA/.qpkg/Duplicati/.config/Duplicati/PJISXRFXEA.sqlite`
3. Rerun the backup itself

If you run into some weird errors, or the backup is still not working rerun `repair`,`list-broken-files` and `purge-broken-files` with the additional option `--no-backend-verification`.
Also rerun the backup itself with the switch set to `true` one time after doing the above. This is some kind of weird user experience problem of duplicati, which was discussed at [Error on purge-broken-files](https://forum.duplicati.com/t/error-on-purge-broken-files/1940) already.

## Links
* [The database file is locked after stopping backup job](https://forum.duplicati.com/t/the-database-file-is-locked-after-stopping-backup-job/3761)
* [Stop after Upload](https://forum.duplicati.com/t/stop-after-upload/3753)
* [Error on purge-broken-files](https://forum.duplicati.com/t/error-on-purge-broken-files/1940)
* [Duplicati](https://www.duplicati.com)
* [Command Line Manual](https://duplicati.readthedocs.io/en/latest/04-using-duplicati-from-the-command-line/#the-list-broken-files-command)
* [Get a backer](https://opencollective.com/duplicati#backer)