---
layout: post
title: Redirect Permalinks from the Main Domain to a Subdomain
date: 2018-06-12
tags: [english, technology]
---

## Background
I migrated my wordpress blog posts from wordpress to jekyll hosted on github successfully. This was a lot of manual work. I decided to use a subdomain for my jekyll site, but the wordpress site was hosted on the main domain `www.feutl.com`. I needed to figure out a way to redirect any permalink from wordpress `www.feutl.com/blogposttitel/` to `blog.feutl.com/blogposttitle/`

Jekyll was already aware of those permalinks used by wordpress, this was not an issue any more, but getting the `.htaccess`file redirect the requests correctly was tricky, especially because `feutl.com` and `www.feutl.com` should not be redirect.

Searching the web for a solution was like searching for the needle in tha haystack. I tested some given solutions by others and came to the conclusion it is much easier to read the manual for [mod_rewrite](https://wiki.apache.org/httpd/Rewrite) and tutorial sites myself and understand what it does.

* [RewriteCond](https://wiki.apache.org/httpd/RewriteCond)
* [RewriteRule](https://wiki.apache.org/httpd/RewriteRule)
* [URL Rewriting for Beginners](https://www.addedbytes.com/blog/url-rewriting-for-beginners)
* [A simple way to understand mod_rewrite](https://mrcoles.com/blog/simple-way-understand-mod-rewrite/)

But the real live saver was the online [.htaccess rewrite rules tester](https://htaccess.madewithlove.be/)

## Problem
This are some of the URLs which needed to be rewritten

url | rewrite 
----|--------
www.feutl.com | www.feutl.com
feutl.com | feutl.com
www.feutl.com/ | www.feutl.com/
www.feutl.com/permalink/ | blog.feutl.com/permalink/
www.feutl.com/permalink | www.feutl.com/permalink
www.feutl.com/blog/ | blog.feutl.com

## Solution
```htaccess
<IfModule mod_rewrite.c>
    RewriteEngine On

    RewriteCond %{REQUEST_URI} ^/blog/$
    RewriteRule ^(.*)$ http://blog.feutl.com [L,R=301,NC]

    RewriteCond %{HTTP_HOST} ^www\.feutl\.com$
    RewriteCond %{REQUEST_URI} ^/(.*)/$
    RewriteRule ^(.*)$ http://blog.feutl.com/$1 [L,R=301,NC]
</IfModule>
```

![.htaccess rewrite rules tester](/img/2018/htaccess-tester.png)