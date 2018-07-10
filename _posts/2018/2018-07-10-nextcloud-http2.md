---
layout: post
title: Using HTTP/2 with Nextcloud
date: 2018-07-06
tags: [english, technology]
---

I used [baytons - Installing Nextcloud on Ubuntu 16.04 LTS+ with Redis, APCu, SSL & Apache ](https://bayton.org/docs/nextcloud/installing-nextcloud-on-ubuntu-16-04-lts-with-redis-apcu-ssl-apache/) to setup the base of Nextcloud. I read quite some articles about migrating Nextcloud from Apache to Nginx. The idea was to save some cpu cycles and memory on my netbook, but the effort and the actual outcome was not worth it. I tested the setup on a virtual machine, to verify if this has any real impact.

The only thing I wanted to accomplish was getting [HTTP/2 working on Apache](https://http2.pro/doc/Apache). It is unclear if this has any positiv performance impact on my setup right now, but at a certain point I need to migrate Nextlcoud to a more performant host anyways and having everything setup already makes it easier.

# Upgrade to PHP 7.2
It has nothing to do with HTTP/2 but I thought it could be quite interesting and future proof to get PHP 7.2 up and running. Especially because PHP 7.0 is EOS with December 2018.

Add ondrej's repository and update

```bash
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
```

Remove PHP 7.0 which automatically replaces it with 7.2 versions and taking care of installing the necessary packages.
```bash
sudo apt-get purge php7.0 php7.0-common

sudo apt-get install php7.2-curl php7.2-xml php7.2-zip php7.2-gd php7.2-mysql php7.2-mbstring php7-dompdf php7.2-curl
```

I did a reboot of the server to be sure everything was applied correctly.
Do not forget to migrate the php.ini configuration from the old php version to the new one, otherwise Nextcloud starts complaining.

## Reference
* [PHP 7.0 to PHP 7.2 - How to upgrade your server](https://jakelprice.com/article/php-70-to-php-72-how-to-upgrade-your-server)

# PHP FastCGI and HTTP/2
To get HTTP/2 properly working with Apache we need to push Apache to 2.4.24 or later and and install PHP FastCGI. I was really surprised how easy this was.

I added once again another repository from ondrej
```bash
sudo add-apt-repository ppa:ondrej/apache2
sudo apt update
sudo apt upgrade
```

I verified if apache still serves my website, installed FPM and enabled/disabled everything necessary.

```bash
sudo apt install php7.2-fpm
sudo a2enmod proxy_fcgi setenvif
sudo a2enconf php7.2-fpm 
sudo a2dismod php7.2
sudo systemctl reload apache2
```

To use HTTP/2 properly we need to change from prefork to event MPM

```bash
sudo a2dismod mpm_prefork
sudo a2enmod mpm_event
sudo systemctl reload apache2
sudo systemctl reload php7.2-fpm
```

After everything is prepared and the Nextcloud is still accessible, it is time to enable Http/2

```bash
sudo a2enmod http2
sudo systemctl reload apache2
```

And add the following to your `apache2.conf` or `site/vhost configuration`

```apache
Protocols h2 h2c http/1.1
````

That's it, using your browsers development tool you can verify the usage of Http/2 for your Nextcloud installation.

## Reference
* [How to Enable HTTP/2 in Apache 2.4 on Ubuntu 16.04](https://techwombat.com/enable-http2-apache-ubuntu-16-04/)
* [How to enable HTTP/2 support in Apache](https://http2.pro/doc/Apache)