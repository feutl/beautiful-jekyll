---
layout: post
title: Text Strings mit PHP kürzen
date: 2006-12-05
tags: [deutsch, technology]
---

Diese Funktion verkürzt einen Text-String auf eine vorgegebene Anzahl von Zeichen und fügt drei Punkte (...) an das Ende. Weiters wird das letzte Wort nicht einfach abgeschnitten sondern als ganzes Wort dargestellt und somit die vorgegebene Zeichenanzahl etwas abgerundet. 

## Beispiel original

> Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

## Beispiel gekürzt
> Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod...

## Code
```php
function ShortenText($text) {
    // Change to the number of characters you want to display 
    $chars = 25;
    $text = $text." ";
    $text = substr($text,0,$chars);
    $text = substr($text,0,strrpos($text,' '));
    $text = $text."...";
    return $text;
}
```