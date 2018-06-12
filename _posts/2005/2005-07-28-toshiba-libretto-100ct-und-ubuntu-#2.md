---
layout: post
title: Toshiba Libretto 100CT & Ubuntu Part 2
date: 2005-07-28
image: /img/2007/libretto-thumb.jpg
tags: [deutsch, technology]
permalink: /toshiba-libretto-100ct-ubuntu-part-2/
---

Das Ziel für heute ist geschafft. Der Windowmanager [fvwm](http://www.fvwm.org/) läuft. Die Auflösung passt und der externe Monitor wird auch mit angesteuert. Einzige Software die ich installiert habe heute war `xterm`. Ich hab keine weiteren Konfigurationen am WM durchgeführt, weils mir einfach viel zu heiß in meinem Arbeitszimmer ist.

Einziges aufgetretenes Problem war die Mausunterstützung. Da der Libretto eine interne Maus besitzt die aber nicht so komfortabel ist wollt ich beide gleichzeitig Benutzen (wenn man mal absteckt). Jedoch wird dann die externe Maus unbedienbar - sie reagiert einfach zu empfindlich, darum empfehle ich den simultanen Modus für das `Pointing Device` im Bios auf `Auto` zu stellen.

Hier noch die Speicherplatznutzung meines Ubuntu-Libretto:

Filesystem | Size | Used | Avail | Use% | Mounted on 
-----------|------|------|-------|------|-----------
/dev/hda1 | 1,8G | 378M | 1,4G | 22% | / 
tmpfs | 15M | 0 | 15M | 0% | /dev/shm
/dev | 1,8G | 378M | 1,4G | 22% | /.dev
none | 5,0M | 2,7M | 2,4M | 54% | /dev

Sodale und jetzt hab ich lust auf ein Eis und geh somit in etwas kühlere Teile meiner Höhle. Eines nur noch, hier kriegt ihr noch die `Xorg.conf` serviert. Xorg.conf ... 


## Xorg.conf
```
Section "ServerLayout"
    Identifier "Default Layout"
    Screen "Default Screen"
    InputDevice "Generic Keyboard" "CoreKeyboard"
    InputDevice "Configured Mouse" "CorePointer
EndSection

Section "Files"
    FontPath "unix/:7100" # local font server
    # if the local font server has problems, we can fall back on these
    FontPath "/usr/lib/X11/fonts/misc"
    FontPath "/usr/lib/X11/fonts/cyrillic"
    FontPath "/usr/lib/X11/fonts/100dpi/:unscaled"
    FontPath "/usr/lib/X11/fonts/75dpi/:unscaled"
    FontPath "/usr/lib/X11/fonts/Type1"
    FontPath "/usr/lib/X11/fonts/CID"
    FontPath "/usr/lib/X11/fonts/100dpi" 
    FontPath "/usr/lib/X11/fonts/75dpi" 
    # paths to defoma fonts 
    FontPath "/var/lib/defoma/x-ttcidfont-conf.d/dirs/TrueType" 
    FontPath "/var/lib/defoma/x-ttcidfont-conf.d/dirs/CID" 
EndSection

Section "Module"
    Load "bitmap" 
    Load "dbe" 
    Load "ddc" 
    Load "dri" 
    Load "extmod" 
    Load "freetype" 
    Load "glx" 
    Load "int10" 
    Load "record" 
    Load "type1" 
    Load "vbe" 
    Load "xtrap" # modified
EndSection

Section "InputDevice"
    Identifier "Generic Keyboard" 
    Driver "keyboard" 
    Option "XkbModel" "pc102" 
    Option "XkbLayout" "de" 
    Option "XkbVariant" "nodeadkeys" 
    Option "XkbRules" "xorg" # modified 
    Option "CoreKeyboard" # modified 
EndSection

Section "InputDevice"
    Identifier "Configured Mouse"
    Driver "mouse"
    Option "Protocol" "auto" 
    Option "Device" "/dev/input/mice" 
    Option "CorePointer" # modified 
    Option "ZAxisMapping" "4 5" # modified
EndSection 

Section "Monitor" 
    #DisplaySize 160 100 mm 
    Identifier "Monitor" VendorName "TOSHIBA" 
    ModelName "Libretto TFT"
    HorizSync 26.0 - 35.0 
    VertRefresh 60.0 - 85.0 
    ModeLine "800x480" 29.59 800 832 944 976 480 490 495 505 
    ModeLine "640x480" 24.11 640 672 760 792 480 490 495 505 
EndSection 

Section "Device" 
    Option "overrideValidateMode" 
    Identifier "Card" 
    Driver "neomagic" 
    VendorName "Neomagic Corporation" 
    BoardName "NM2160 [MagicGraph 128XD]" 
    BusID "PCI:0:4:0" 
EndSection

Section "Screen"
    Identifier "Default Screen"
    Device "Card"
    Monitor "Monitor"
    DefaultDepth 16
    
    SubSection "Display"
        Viewport 0 0
        Depth 1
    EndSubSection
    SubSection "Display"
        Viewport 0 0
        Depth 4
    EndSubSection
    SubSection "Display"
        Viewport 0 0
        Depth 8
    EndSubSection
    SubSection "Display"
        Viewport 0 0
        Depth 15
    EndSubSection
    SubSection "Display"
        Viewport 0 0
        Depth 16 Modes "800x480" "640x480"
    EndSubSection
    SubSection "Display"
        Viewport 0 0
        Depth 24
    EndSubSection
EndSection
```