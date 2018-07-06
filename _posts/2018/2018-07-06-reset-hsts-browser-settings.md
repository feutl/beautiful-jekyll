---
layout: post
title: Reset HTTP Strict Transport Security Browser Settings
date: 2018-07-06
tags: [english, technology]
---

If you are having issues using websites with the restrictive HSTS (HTTP Strict Transport Security) settings, for whatever reason this browser specific methods may help.

# .htaccess
Setting the expiration time on the HSTS header to zero should immediatly make it expire.

```
<IfModule mod_headers.c>
   Header set Strict-Transport-Security "max-age=0; includeSubDomains;" env=HTTPS
</IfModule>
```

# Chrome
1. In the address bar, type “chrome://net-internals/#hsts”.
2. Type the domain name in the text field below “Delete domain”.
3. Click the “Delete” button.
4. Type the domain name in the text field below “Query domain”.
5. Click the “Query” button.
6. Your response should be “Not found”.
7. Quit Chrome then relaunch and test.

# Firefox
1. First, you need to close all open windows
2. Goto Browser Settings --> History. Select "Show All/Complete History" or `Ctrl + Shift + H (Cmd + Shift + H on Mac)`
3. Go to the site for which you want to clear HSTS settings
4. Now right-click on that site and then click on Forget About This Site.
   * Keep in mind that this will clear all data of the site present in Firefox.

### Advanced Method
* Find file SiteSecurityServiceState.txt typically located in C:\Users\username\AppData\Roaming\Mozilla\Firefox\Profiles\ 
* Edit the file and delete the line that starts with "yourdomain.com".

# Safari
1. Quit Safari.
2. Delete the file ~/Library/Cookies/HSTS.plist.
3. Reopen Safari.

# Internet Explorer / Edge
The only supported method of removing site specific HSTS settings is to revisit the site and load the new HSTS directives.

Microsoft uses preload lists for HSTS which results in the known behavior
> Site developers can use HSTS policies to secure connections by opting in to an HSTS preload list, which registers websites to be hardcoded by Microsoft Edge, Internet Explorer, and other browsers to redirect HTTP traffic to HTTPS. Communications with these websites from the initial connection are automatically upgraded to be secure. Like other browsers which have implemented this feature, Microsoft Edge and Internet Explorer 11 base their preload list on the Chromium HSTS preload list.
 
While disabling HSTS altogether is NOT recommended, doing so temporarily may be helpful for testing:
https://support.microsoft.com/en-us/help/3071338/internet-explorer-11-adds-support-for-http-strict-transport-security-standard

### For x64-based systems
1. Click Start, click Run, type regedit, and then click OK.
2. Locate the following registry subkey: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Internet Explorer\Main\FeatureControl\`
3. On the Edit menu, point to New, and then click Key.
4. Type FEATURE_DISABLE_HSTS, and then press Enter.
5. Click `FEATURE_DISABLE_HSTS`
6. On the Edit menu, point to New, and then click DWORD value.
7. Type iexplore.exe.
8. On the Edit menu, click Modify
9. In the Value data box, type 1, and then click OK.
   * Note The valid values for the iexplore.exe subkey are 0 and 1. A value of 1 disables the feature, and 0 enables the feature.
10. Locate the following registry subkey: `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Internet Explorer\Main\FeatureControl\`
11. On the Edit menu, point to New, and then click Key.
12. Type FEATURE_DISABLE_HSTS, and then press Enter.
13. Click `FEATURE_DISABLE_HSTS`
14. On the Edit menu, point to New, and then click DWORD value.
15. Type iexplore.exe.
16. On the Edit menu, click Modify.
17. In the Value data box, type 1, and then click OK.
    * Note The valid values for the iexplore.exe subkey are 0 and 1. A value of 1 disables the feature, and 0 enables the feature.
18. Exit Registry Editor.

# General HSTS Information
* [https://www.troyhunt.com/understanding-http-strict-transport/](Understanding HTTP Strict Transport Security and preloading it into the browser)
* [https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet](HTTP Strict Transport Security Cheat Sheet)
* [https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security](HTTP Strict Transport Security)
* [https://blogs.windows.com/msedgedev/2015/06/09/http-strict-transport-security-comes-to-internet-explorer-11-on-windows-8-1-and-windows-7/](HTTP Strict Transport Security comes to Internet Explorer 11 on Windows 8.1 and Windows 7)