---
layout: post
title: Invalid PHP_SELF Path & Cacti & Ubuntu 7.10
date: 2008-03-26
tags: [deutsch, technology]
permalink: /invalid-php_self-path-cacti-ubuntu-710/
---

Wenn nach der Installation oder Update Cacti mit oben genannten Error aufwartet hilft das Anpassen der `/usr/share/cacti/site/include/config.php`

Man ersetzt den Teil zw. `/* Sanity Check on "Corrupt" PHP_SELF */` und `/* we don't want these pages cached */` mit:

```php
if ((!is_file($_SERVER["PHP_SELF"])) &amp;&amp; (!is_file($config["base_path"] . '/' . $_SERVER["PHP_SELF"]))) {
    if (!is_file($_SERVER["DOCUMENT_ROOT"] . $_SERVER["PHP_SELF"])) {
        if (!((is_file($_SERVER["SCRIPT_FILENAME"])) &amp;&amp; (substr_count($_SERVER["SCRIPT_FILENAME"], $_SERVER[$
            if (!((is_file($_SERVER["SCRIPT_FILENAME"])))) {
                echo "\nInvalid PHP_SELF Path\n";
                exit;
            }
        }
    }
}

[A Cacti Bug](https://bugs.launchpad.net/ubuntu/+source/cacti/+bug/194687)