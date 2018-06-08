---
layout: post
title: Link Collection - Storage 
date: 2005-11-21
tags: [english, technology]
---

## General
*   [My posts categorized in Storage](http://blog.feutl.com/category/storage-2/)
*   [Anatomy of an Ethernet Frame for Storage Guys](https://communities.netapp.com/blogs/ethernetstorageguy/2009/09/12/anatomy-of-an-ethernet-frame)
*   [ZFS Community Group](http://hub.opensolaris.org/bin/view/Community+Group+zfs/)
*   [OpenFiler](http://openfiler.com/)
*   [FreeNAS](http://www.freenas.org/)
*   [Debian on QNAP TS-109](http://www.cyrius.com/debian/orion/qnap/ts-109/)
*   [A couple important (ALUA and SRM) notes](http://virtualgeek.typepad.com/virtual_geek/2009/09/a-couple-important-alua-and-srm-notes.html)
*   [What’s that ALUA exactly?](http://www.yellow-bricks.com/2009/09/29/whats-that-alua-exactly/ "What’s that ALUA exactly?")

## NetApp Specific
*   [NetApp TV Channel](http://www.youtube.com/user/NetAppTV?feature=watch)
*   [NetApp Community](https://communities.netapp.com/welcome)
*   [Data ONTAP Simulator Installation Simple Steps and Frequently Asked Questions](http://communities.netapp.com/blogs/fitforpurpose/2009/09/06/data-ontap-simulator-installation-simple-steps-and-frequently-asked-questions)

## Alignment
*   [5 Reasons to Upgrade to Data Ontap 8.0.1](http://communities.netapp.com/community/netapp-blogs/virtualstorageguy/blog/2011/03/25/5-reasons-to-upgrade-to-data-ontap-801)
*   [Aligning your VMs virtual hard disks](http://www.yellow-bricks.com/2010/04/08/aligning-your-vms-virtual-harddisks/ "Aligning your VMs virtual hard disks")
*   [How to create aligned partitions in Linux for use with NetApp LUNs, VMDKs, VHDs and other virtual disk containers](https://kb.netapp.com/support/index?page=content&id=1010717)
*   [LUN Types and Linux partition alignment](http://netapptips.com/2010/03/16/lun-types-and-linux-partition-alignment/)
*   [Initiator Types (what are they for) and LUN Types - Hyper-V](http://communities.netapp.com/message/21212#21212)
*   [Q&S (Quick and simple) - How to align misaligned VMs on a ESXi4 or ESXi5 Host with NetApp MBRTools](http://mynetapp.de/buch/qamps-quick-and-simple-how-align-misaligned-vms-esxi4-or-esxi5-host-netapp-mbrtools)

## Tag Explanation
*   [Fibre Channel](http://en.wikipedia.org/wiki/Fibre_Channel) Fibre Channel, or FC, is a gigabit-speed network technology primarily used for storage networking. Fibre Channel is standardized in the T11 Technical Committee of the InterNational Committee for Information Technology Standards (INCITS), an American National Standards Institute (ANSI)–accredited standards committee. Fibre Channel was primarily used in the supercomputer field, but now, has become the standard connection type for storage area networks (SAN) in enterprise storage. Despite its name, Fibre Channel signaling can run on both twisted pair copper wire and fiber-optic cables. Fibre Channel Protocol (FCP) is a transport protocol (similar to TCP used in IP networks) which predominantly transports SCSI commands over Fibre Channel networks.
*   [FLOGI / PLOGI /PRLI (taken from EMC Community Network)](https://community.emc.com/message/432236#432236) 
    * N_Portan
    end device connecting to a switched fabric network, such as a SCSI initiator or a SCSI target.
    * F_Port
    a port on a switch that provides access to Fabric Services (eg. the Fabric Nameserver & the Fabric Login Server etc)Fabric_point_2_point initialization (ie. N_Port to F_Port initialization) involves the following ordered sequence: FLOGI, PLOGI, PRLI.
    * FLOGI
    N_Port requests a unique 24-bit address from the Fabric Login Server (accessible via an F_port on a Fabric switch).#
    * PLOGI
    N_Port informs the Fabric Name Server of its personality and capabilities.
    For example:
        * WWNN, WWPN 
        * Buffer credits for flow control
        * clock frequency ('speed capability') 
        * Upper layer protocol support (eg. SCSI-3, IP)
    * PRLI
    Upper layer protocol communication. Well, ever since SCSI was designed and engineered (1970s, or so, previously SASI...), SCSI initiators need to discover SCSI targets. So, during PRLI, N_Port SCSI initiators discover N_Port SCSI targets (which is an opportunity for the host (maybe a UNIX host) to assign a target ID to the device path). Depending on the OS, you may be able to investigate further with commands like: `egrep -i 'flogi|plogi|prli' /var/adm/messages`