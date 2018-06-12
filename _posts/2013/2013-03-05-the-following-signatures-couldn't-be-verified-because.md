---
layout: post
title: The following signatures couldn't be verified because the public key is not available
date: 2013-03-05
tags: [english, technology]
---

Ubuntu is nice to use, it works flawlessly on most systems. Especially the packet management is awesome and therefore I wanna say thanks to Debians developers for that. 

What so ever, sometimes you have to add a Repository to the sources.list which creats a failure during fetching the package data. The failure most of the time is based on a not verified public key. To get rid of that there are a few steps to do:

`GPG error: http://ppa.launchpad.net intrepid Release: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 28A8205077558DD0`

```bash
sudo gpg --keyserver x-hkp://pool.sks-keyservers.net --recv-keys 28A8205077558DD0
sudo gpg --export --armor 28A8205077558DD0 | sudo apt-key add -
```
Be aware that you should only add keys if you really trust the repository. 

## Update
A shorter version to add keys of a repository using one command:
`sudo apt-key adv --recv-keys --keyserver keyserver.ubuntu.com 28A8205077558DD0`