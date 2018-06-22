---
layout: post
title: Migrate to Nextcloud
subtitle: Take Control Over Your Digital Life
date: 2018-06-22
tags: [english, technology, nextcloud, privacy]
bigimg: /img/2018/htop-nextcloud-standby.png
---

> Great Things Never Came From Comfort Zones.

I am IT administrator for a small company called "Family" and I also feel it as my obligation to enforce some level of privacy. As technology grows and invades every part of our private lives, we hand over private information without thinking twice. But on the other hand, it is easier than ever to take back that control and data.

Software, technology, and people have not only created outstanding services used on a daily basis, they also allow us to run and host services reliably at home or wherever you feel your data is save. It was never easier, everything you need is the courage to start reading, asking some questions and to follow your own curiosity.

This was the reason, why I started to migrate parts of my family network from [Resilio Sync](https://www.resilio.com/individuals/) to [Nextcloud](https://www.nextcloud.com). In contrary to Resilio Sync, Nextcloud allows not only to keep my data private, which I had already accomplished with Sync, but give my family a simple option to view, edit, update and most important - share - data.

Sharing data was something I haven't considered as important, because I just do not share much data with others, but the rest does. And as more pictures are being created and  organized directly on mobile phones, this was something to address. Not addressing it, already lead to uploading files to services like [OneDrive](https://onedrive.live.com/), [Dropbox](https://www.dropbox.com) and others - which means loosing data I initially wanted to keep private.

# Setup
I took an old netbook (Medion Akoya S1210) and installed Ubuntu 16.04 LTS on it. Because of the limited resources of the netbook, the nextcloud user data needs to be "outsourced" and therefore I am using a NAS via a permanent NFS mount.

# Installation
## Base System
Ubuntu and Nextcloud

* [System Requirements](https://docs.nextcloud.com/server/13/admin_manual/installation/system_requirements.html)
* [Ubuntu 16.04.4 LTS (Xenial Xerus)](http://releases.ubuntu.com/16.04/)
* [Installing Nextcloud on Ubuntu 16.04 LTS+ with Redis, APCu, SSL & Apache](https://bayton.org/docs/nextcloud/installing-nextcloud-on-ubuntu-16-04-lts-with-redis-apcu-ssl-apache/)
* [How To Install and Configure Nextcloud on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-nextcloud-on-ubuntu-16-04)
* [How to Install NextCloud Server on Ubuntu 16.04](https://www.youtube.com/watch?v=nXr_muYB6xI)
* [Snappy Nextcloud](https://github.com/nextcloud/nextcloud-snap)\\
This is not being used, because I needed to have the option to mount SMB/CIFS shares, and this is not supported with the nextcloud snap yet.

# Configuration
## NFS Datastore
I am using a NAS via NFS as a datastore

* [Change data directory to use another disk partition](https://github.com/nextcloud/nextcloud-snap/wiki/Change-data-directory-to-use-another-disk-partition)\\
Even though I am not using the nextcloud snap, the information is still useful
* [Setting Up NFS](https://help.ubuntu.com/community/SettingUpNFSHowTo)\\
I am using NFS instead of SMB mounts because it was just easier to setup\\
`192.168.11.10:/Nextcloud  /media/nextcloud-data  nfs  rw  0  0`
* [Mount Windows Shares Permanently](https://wiki.ubuntu.com/MountWindowsSharesPermanently)\\
Even not using it, it could be useful to know how it works.

## Background Jobs
I changed this to cron (daemon). Nextclouds webinterface is not accessed that often therefor the default method "AJAX" just doesn't make much sense. Also having full access to the underlying OS makes this even possible.

* [Defining background jobs](https://docs.nextcloud.com/server/13/admin_manual/configuration_server/background_jobs_configuration.html)

# Migration
## WebDAV
I am using WebDAV to migrate data from the old way data was synced and stored to Nextcloud. The data gets immediately recognized and no OCC scripts need to be executed.

* [Accessing Nextcloud files using WebDAV](https://docs.nextcloud.com/server/13/user_manual/files/access_webdav.html)\\
`net use Z: \\example.com@ssl\nextcloud\remote.php\dav /user:youruser yourpassword`

* [File Operations](https://docs.nextcloud.com/server/13/admin_manual/configuration_server/occ_command.html#file-operations-label)\\
You could also copy the files directly on the OS/filesystem layer and index them using nextcloud command line afterwards\\
`sudo -u www-data php occ files:scan --all`

# House-Keeping
## Hardening Nextcloud
Hosting a service, which can be accessed publicly, needs some house-keeping. Hardening the service and operating system, luckily most of the things are already configured out-of-the box or only need special attention if you widen access from the outside.

* [Hardening and security guidance](https://docs.nextcloud.com/server/13/admin_manual/configuration_server/harden_server.html)
* [Best practices for hardening new sever in 2017](https://www.digitalocean.com/community/questions/best-practices-for-hardening-new-sever-in-2017)
* [Harden Ubuntu security for 16.04 server (The Complete Guide)](https://poweruphosting.com/blog/ubuntu-security/)

## Security / Vulnerability Scans
Ways to verify your hardening was successful and are secure. Doing this is still not guaranteeing that you never get compromised.

* [Check the security of your private Nextcloud server](https://scan.nextcloud.com/)
* [SSL Server Test](https://www.ssllabs.com/ssltest/index.html)
* [Let's Encrypt](https://www.letsencrypt.com)
* [Barracuda Vulnerability Manager](https://bvm.barracudanetworks.com)

## Network Firewall
It makes sense to use a firewall to secure hosted services as well as your network.

* [Barracuda CloudGen Firewall](https://www.barracuda.com/products/nextgenfirewall_f)
* [OPNsense](https://opnsense.org/)

## Backup
Nothing to add here

* [Nextcloud 13 backup and restore](https://www.c-rieger.de/nextcloud-backup-and-restore/)
** Turn maintenance mode on: `sudo -u www-data php /var/www/nextcloud/occ maintenance:mode --on`
** Backup the webfolder: `tar -cpzf /home/ubuntuusername/ncserver_`date +"%w"`.tar.gz -C /var/www/nextcloud .`
** Backup the datafolder: `tar -cpzf /home/ubuntuusername/ncdata_`date +"%w"`.tar.gz -C /var/nc_data .`
** Backup the database: `mysqldump --single-transaction -h localhost -unextcloud -pnextcloud nextcloud > /home/ubuntuusername/ncdb_`date +"%w"`.sql`
** Turn maintenance mode off: `sudo -u www-data php /var/www/nextcloud/occ maintenance:mode --off`

# Useful
## Command Line
* [Using Nextcloud’s command line](https://www.c-rieger.de/using-nextclouds-command-line/#eins)
