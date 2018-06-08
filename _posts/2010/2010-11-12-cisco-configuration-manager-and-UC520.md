---
layout: post
title: Cisco Configuration Manager and UC520
date: 2011-11-12
tags: [english, technology, cisco]
image: /img/2007/cisco.gif
---

After downloading the newest version of [Ciscos Configuration Manager](https://supportforums.cisco.com/docs/DOC-10988) and all the updated packages for the UC520 I started the upgrade process for the [Unified Communications 520 for Small Business](http://www.cisco.com/en/US/prod/collateral/voicesw/ps6788/vcallcon/ps7293/product_data_sheet0900aecd8061fb06.html). I wasn't surprised when the first error messages came up, because those things never work that smoothly.

Nevertheless, the thing that pissed me off were the actual error messages which did not tell me anything, after 2 days and about 5 retries to upgrade the machine I digged around and found a how-to for a manual update process - my last resort!

After leaning back in my chair I tried something different and that worked out smoothly. The unclear error messages I got were all based on one fact - there was to less space on my flash card (why did nobody tell me that).

So there are 2 ways to upgrade your UC520 withouth problems

1. format/erase your 128 MB flash card located in your UC (or take a new one) using the CCA and after that, start the upgrade process and it will work - smoothly as expected
2. Follow the forum thread for a manual upgrade without using CCA (which can also be used on operating systems not have the possibility to run CCA)

## Resources
* [UC upgrade manually without CCA](https://supportforums.cisco.com/message/3082911#3082911)