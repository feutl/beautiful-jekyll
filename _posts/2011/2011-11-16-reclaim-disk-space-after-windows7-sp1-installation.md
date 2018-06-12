---
layout: post
title: Reclaim disk space after Windows 7 SP1 installation
date: 2011-11-16
tags: [english, technology]
permalink: /reclaim-disk-space-after-windows-7-sp1-installation/
---

Did you ever heard about the WINSXS folder on your system? If not, it is now a good time to check the size of it. A few GB of disk space are used for a folder nobody knows why it is there at all. 

The same situation applied to me, but after reading a few sites and blog entries I do know that it is important. It is storing all needed components Windows 7 needs during its life time. The idea is to hard link them from any place - so only one location is needed and no duplicates are created. Well, that is an awesome idea, but what Windows 7 is not doing - cleaning up! After you have installed SP1 for Windows 7 - some of these components are not needed any more - but the remain in the folder - the only reason is - if you would uninstall the SP1 the superseeded components can be reactivated. 

I decided there is no need for that behaviour and using the tool DISM on the command line - all the superseeded components get deleted. Only "downside": you can not uninstall SP1 from this point onwards 

The command I used to reclaim my disk space after updating my Windows 7 to SP1 with Windows Update

`dism /Online /Cleanup-Image /spsuperseded`

[How to reclaim space after applying Windows 7/2008 R2 Service Pack 1](https://blogs.technet.com/themes/blogs/generic/post.aspx?WeblogApp=joscon&y=2011&m=02&d=15&WeblogPostName=how-to-reclaim-space-after-applying-service-pack-1&GroupKeys=) [WinSXS](http://answers.microsoft.com/en-us/windows/forum/windows_vista-performance/winsxs/e473cda6-94d5-4e6a-9ce8-97cf876174a0)