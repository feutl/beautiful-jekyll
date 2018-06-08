---
layout: post
title: Toshiba Libretto 100CT und FreeBSD 4
date: 2007-07-22
tags: [deutsch, technology]
img: /img/2007/libretto-thumb.jpg
---

Nach langem arbeiten hab ich eine einfach Version von FreeBSD 4.11 auf meinem Libretto am Laufen. Auf Grund meiner Versuche sprang der Kollege "matze" mit auf den Zug auf und mit seinen fundierten Linux und BSD Kenntnissen erzielte er erfolge für die ich als Newbie noch einige Monate gebraucht hätte. Zusammen haben wir dann folgende Anleitung zusammengefasst um jeden die Möglichkeit zu geben seinem Libretto eine FreeBSD 4 zu verpassen


![Libretto 100CT](/img/2007/libretto.jpg)

## Technische Daten
### Prozessor / Bus /RAM
*   Prozessor Intel Pentium 166 MHz MMX / 1.8 V
*   Bus 66 MHz
*   Cache-Speicher Write-Back / 32 KB auf CPU
*   Speicher (RAM) 32 MB EDO / 60 ns / 2.5 V / max. 64 MB

### BIOS
*   Typ Flash-EPROM / Plug&Play / APM / ACPI / 512 KB

### Grafik
*   Typ NeoMagic MagicGraph 128 XD / PCI / 128 Bit Grafikbeschleuniger
*   Video-RAM 2 MB
*   Bildschirm TFT
*   Bildpunkte 800 x 480 Pixel
*   Pixelgrösse 0.19 x 0.19 mm
*   Diagonale 7.1"
*   Darstellungsbereich 153.6 x 93 mm
*   Farben bis 16 Millionen / 24 Bit
*   Kontrastverhältnis 100:1
*   LCD-Helligkeit (Netzbetrieb) 70 NIT
*   LCD-Helligkeit (Akkubetrieb) 70 NIT

### Bildschirmauflösungen
*   Max. intern 24 Bit Farbe 640 x 480 / 85 Hz
*   Max extern 16 Bit Farbe 1024 x 768 / 85 Hz
*   Max extern 24 Bit Farbe 800 x 600 / 85 Hz

### Maße und Gewicht
*   Abmessung 210 x 132 x 34 mm
*   Gewicht 910 g

### Akku
*   Typ Li-Ion / 10.8 V / 1200 mAh
*   Max. Betriebsdauer 2 h

### Netzadapter
*   Typ 100-240 VAC / 50-60 Hz
*   Ausgang 15 V / 2 A
*   Gewicht 180 g

### Festplatte
*   Typ Toshiba MK-2109MAT / 2.1 GB / 13 ms / 4200 U/min
*   Schnittstelle E-IDE / AT-kompatibel

### Diskettenlaufwerk
*   Typ Extern PCMCIA / 3,5" / 720 KB + 1.44MB / 300 U/min

### Sound
*   Am PC Lautsprecher Mono / Mikrofon
*   Typ Yamaha OPL3 SA3 / 16-Bit Stereo / Soundblaster-kompatibel / MIDI

### Anschlüsse
*   Am PC Kopfhörer / Mikrofon / PCMCIA Type III / Infrarot / Netzadapter
*   Miniport Replicator (Lieferumfang) Seriell / Parallel (ECP) / PS/2 / Monitor / Netzadapter
*   Mini Card Station (Zubehör) Seriell / Parallel (ECP) / PS/2 / Monitor / PCMCIA Type III / Netzadapter / USB

### Installation

Die Installation funktioniert mit FreeBSD 4.11 problemlos über zwei zu erstellende Disketten.

> __Hinweis:__ Diese Installationsweise ist mit FreeBSD 5.x nicht mehr möglich, da es hier eine Änderung in der Installationsroutine von _sysinstall_ gab und somit somit bei der Installation nicht mehr automatisch erkannt wird, dass es sich beim Installlationsmedium um ein PCMCIA Device handelt. FreeBSD 5.x fragt somit nicht mehr nach ob das Installationmedium im PCMCIA Slot gegen ein andere Gerät getauscht werden soll. Somit muss man Disklaufwerk und CD-Rom oder NIC gleich von anfang an in den Slots haben.

### Diskimages

Zunächst besorgen wir uns die dafür Notwendigen Images:
* [Disk1](ftp://ftp6.freebsd.org/pub/FreeBSD/releases/i386/4.11-RELEASE/floppies/kern.flp "ftp://ftp6.freebsd.org/pub/FreeBSD/releases/i386/4.11-RELEASE/floppies/kern.flp")
* [Disk2](ftp://ftp6.freebsd.org/pub/FreeBSD/releases/i386/4.11-RELEASE/floppies/mfsroot.flp "ftp://ftp6.freebsd.org/pub/FreeBSD/releases/i386/4.11-RELEASE/floppies/mfsroot.flp")

#### Windows

Man braucht für Windows natürlich wieder ein extra Tool: [fdimage](ftp://ftp6.freebsd.org/pub/FreeBSD/releases/i386/4.11-RELEASE/tools/fdimage.exe "ftp://ftp6.freebsd.org/pub/FreeBSD/releases/i386/4.11-RELEASE/tools/fdimage.exe") Der Befehl zum Schreiben lautet
`fdimage.exe kern.flp a:`

#### Linux
' dd if=/kern.flp bs=18k of=/dev/fd0' 

### FreeBSD
`dd if=floppies/kern.flp of=/dev/rfd0`
oder
`dd if=floppies/kern.flp of=/dev/floppy`

Nach dem erfolgreichen erstellen der Disketten gibt es zwei Möglichkeiten zur weitern Installation.

Entweder man verwendet eine PCMCIA Ethernet Karte (z.B. NE2000 kompatibel) zur Installation via FTP, oder man ist im Besitz eines externen CD-ROM Laufwerkes, welches natürlich auch per PCMCIA angeschlossen wird. Da die Softwareauswahl auf den CD's begrenzt ist und unsere favorisierten Programme gar nicht enthält, empfehle ich die Installation über FTP. Auf den genauen Ablauf der weiteren Installation möchte ich an dieser Stelle nicht weiter eingehen, darüber gibt es bereits genug HowTo's. Sie verläuft genauso, wie auf anderen Rechnern auch. 

Egal welche Installationsmöglichkeit ihr wählt, wenn ihr die im Libretto Hardwaremäßig integrierte Hibernate verwenden wollt müsst ihr am Ender eurer HDD einen unpartitionierten Platz in der Größe eures RAM Speichers lassen. Solltet ihr das nicht tun und Hibernate verwenden könnte es leicht passieren das euer System flöten geht.

Da das kompilieren auf der Libretto nicht wirklich Freude macht, empfehle ich grundlegend die Installation von Packages und nur im Notfall die Ports. Die Packages können nach erfolgreich abgeschlossener Installation problemlos als root per _/stand/sysinstall_ nachinstalliert werden oder auch direkt mittels `pkg_add -r name`.

## Xfree86
Folgende Beispiel Konfiguration bildet später eine Auflösung bei 800x480 Bildpunkten und 60 Hz ab:

```
Section "ServerLayout"
    Identifier "XFree86 Configured"
    Screen 0 "Screen0" 0 0
    InputDevice "Mouse0" "CorePointer"
    InputDevice "Keyboard0" "CoreKeyboard"
EndSection

Section "Files"
    RgbPath "/usr/X11R6/lib/X11/rgb"
    ModulePath "/usr/X11R6/lib/modules"
    FontPath "/usr/X11R6/lib/X11/fonts/misc/"
    FontPath "/usr/X11R6/lib/X11/fonts/TTF/"
    FontPath "/usr/X11R6/lib/X11/fonts/Speedo/"
    FontPath "/usr/X11R6/lib/X11/fonts/Type1/"
    FontPath "/usr/X11R6/lib/X11/fonts/CID/"
    FontPath "/usr/X11R6/lib/X11/fonts/75dpi/"
    FontPath "/usr/X11R6/lib/X11/fonts/100dpi/"
EndSection

Section "Module"
    Load "dbe"
    Load "dri"
    Load "extmod"
    Load "glx"
    Load "record"
    Load "xtrap"
    Load "speedo"
    Load "type1"
EndSection

Section "InputDevice"
    Identifier "Keyboard0"
    Driver "keyboard"
    Option "XkbModel" "pc102"
    Option "XkbLayout" "de"
    Option "XkbVariant" "nodeadkeys"
EndSection

Section "InputDevice"
    Identifier "Mouse0"
    Driver "mouse"
    Option "Protocol" "auto"
    Option "Device" "/dev/sysmouse"
EndSection

Section "Monitor"
    #DisplaySize 160 100 mm
    Identifier "Monitor0"
    VendorName "TOSHIBA"
    ModelName "Libretto TFT"
    HorizSync 26.0 - 35.0
    VertRefresh 60.0 - 85.0
    ModeLine "800x480" 29.59 800 832 944 976 480 490 495 505
    ModeLine "640x480" 24.11 640 672 760 792 480 490 495 505
EndSection

Section "Device"
    Option "overrideValidateMode"
    Identifier "Card0"
    Driver "neomagic"
    VendorName "Neomagic Corporation"
    BoardName "NM2160 [MagicGraph 128XD]"
    BusID "PCI:0:4:0"
EndSection

Section "Screen"
    Identifier "Screen0"
    Device "Card0"
    Monitor "Monitor0"
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
        Depth 16
        Modes "800x480" "640x480"
    EndSubSection

    SubSection "Display"
        Viewport 0 0
        Depth 24
    EndSubSection
EndSection
```

### Externer Monitor
Ich habe noch keine Möglichkeit gefunden, das LCD während dem arbeiten auf einen externen Monitor zu switchen. Einzige Möglichkeit auf einen externen Monitor auszugeben ist, den Monitor schon beim booten einstecken. Dabei wird das LCD allerdings ausgeschaltet.

## Sound
Folgende Hardware Einstellungen sind Standard im BIOS:

```
Sound = EnableWSS I/O Address = 530H
SBPro I/O Address = 220H
Synthesizer I/O Address = 388H
WSS & SBPro & MPU401 IRQ Level = IRQ5
WSS(Play) DMA = Channel 1
SBPro DMA = Same as WSS
Control I/O Address = 370H
MPU401 (MIDI I/F) = 330H</pre>
```

Es gibt zwei Möglichkeiten, entweder man baut einen neuen Kernel, oder man erzeugt eine separate Konfigurations Datei

### Variante 1 (neuer Kernel)
Na dann lass uns mal einen neuen Kernel backen. Voraussetzung ist, dass du die Sourcen in _/usr/src_ installiert hast, was normalerweise der Fall sein sollte.

Sollte das jedoch nicht der Fall sein kannst du dir die Sources wie folgt nachinstallieren. Zuerst rufst du _/stand/sysinstall_ auf und gehst dort auf _/configure/distributions/src/sys_ danach einfach _OK_ auswählen und ein bißchen warten bis alles installiert ist - von da an sollte _/usr/src_ vorhanden sein.

> **Alles folgende als root ausführen!!**

```
# cd /usr/src/sys/i386/conf# cp GENERIC MYKERNEL
# echo "device pcm0 at isa? port 0x530 irq 5 drq 1 flags 0" >> MYKERNEL
```

Kernel backen
```
# config MYKERNEL# cd ../../compile/MYKERNEL
# make depend && make && make install && make clean
# shutdown -r now</pre>
```

Jetzt sollte unter _dmesg_ ein Device _pcm0_ auftauchen. Die Ausgabe von _cat /dev/sndstat_ sieht dann so aus:
```
FreeBSD Audio Driver (newpcm)Installed devices:
pcm0: <OPL3-SAx (YMF719)> at io 0x530 irq 5 drq 1 bufsz 4096 (1p/1r/0v channels duplex)
```

Nur noch schnell die Devices in _/dev_ erstellen mit:
`# cd /dev# sh MAKEDEV snd0`

> **Hinweis:** Und bitte keine Sound Module beim Systemstart laden!

### Variante 2 (Konfigurations-Datei)
* Kernel vorbereiten

`device pcm`

Einfach diesen eintrag in eurer neuen Kernel-Config dazuschreiben und den Kernel wie bei Variante 1 beschrieben neu bauen.
* Konfigurationsdatei /boot/device.hints anpassen
```
hint.pcm.0.at="isa"hint.pcm.0.port="0x530"
hint.pcm.0.irq="5"
hint.pcm.0.drq="1"
hint.pcm.0.flags="0x0"</pre>
```

* Neustart
`shutdown -r now`
Jetzt sollte unter _dmesg_ ein Device _pcm0_ auftauchen. Nur noch schnell die Devices in _/dev_ erstellen mit:
`# cd /dev# sh MAKEDEV snd0`

## PowerManagement
### APM aktivieren

*   Kernel vorbereiten
`device apm`

Einfach diesen eintrag in eurer neuen Kernel-Config dazuschreiben und den Kernel wie beim Kapitle Sound Variante1 beschrieben neu bauen oder ihr nehmt einfach die Beispiel Kernel-Config - dort ist schon alles drin.

* Konfigurationsdatei /etc/rc.conf anpassen
```
apm_enable="YES"apmd_enable="YES"
apmd_flags=""</pre>
```

* Konfigurationsdatei `/boot/device.hints` anpassen
```
hint.acpi.0.disabled="1"hint.apm.0.disabled="0"
hint.apm.0.flags="0x20"</pre>
```

* Ausschalten mit automatischem Herunterfahren
`shutdown -p now`

* Jetzt muss der Benutzer nur noch der Gruppe 'operator' hinzugefügt werden:
`pw usermod <username> -G operator`

* eventuelle Fehler Meldungen
> bei Meldung _/dev/apm_ nicht vorhanden _/boot/device.hints_ überprüfen ob bei _hint.apm.0.disabled="0"_ steht

## IrDA
Die Infrarot Schnittstelle unter _dmesg_:
`chip1: <Toshiba Fast Infra Red controller> port 0xffe0-0xffff irq 11 at device 17.0 on pci0`

Das Programm birda (pgk_add -r birda), welches für die Kommunikation mit Infrarot-Geräten (Palm) zuständig ist, sollte installiert werden._ Das Syncronisieren eines Palm mit einer UNIX Workstation geht dann z.B. mit dem Programm _coldsync_ (pkg_add -r coldsync).

## Diskettenlaufwerk
Das PCMCIA Diskettenlaufwerk des Librettos hat schon mancher Linux-Distribution bei der Installation von Diskette das Leben schwer gemacht. *BSD ist da besser und macht keine größeren Probleme bei der Installation doch bei laufendem System wills noch nicht klappen.

## Kernel Config
Hier unsere Kernel-Config, sie ist nicht perfekt und erfüllt auch nicht alle wünsche - also sie ist kein AllHeilMittel. Doch für den Anfang sehr brauchbar und lässt den Libretto in der Standardkonfiguration zum Leben erwachen. Doch für Tipps und Anpassungsvorschläge sind wir immer dankbar.

```
machine		i386cpu		I586_CPU
ident		libretto
maxusers	10options 	INET			#InterNETworking
options 	INET6			#IPv6 communications protocols
options 	FFS			#Berkeley Fast Filesystem
options 	FFS_ROOT		#FFS usable as root device [keep this!]
options 	SOFTUPDATES		#Enable FFS soft updates support
options 	UFS_DIRHASH		#Improve performance on big directories
options 	MFS			#Memory Filesystem
options 	MD_ROOT			#MD is a potential root device
options 	NFS			#Network Filesystem
options 	NFS_ROOT		#NFS usable as root device, NFS required
options 	MSDOSFS			#MSDOS Filesystem
options 	CD9660			#ISO 9660 Filesystem
options 	CD9660_ROOT		#CD-ROM usable as root, CD9660 required
options 	PROCFS			#Process filesystem
options 	COMPAT_43		#Compatible with BSD 4.3 [KEEP THIS!]
options 	SCSI_DELAY=15000	#Delay (in ms) before probing SCSI
options 	UCONSOLE		#Allow users to grab the console
options 	USERCONFIG		#boot -c editor
options 	VISUAL_USERCONFIG	#visual boot -c editor
options 	KTRACE			#ktrace(1) support
options 	SYSVSHM			#SYSV-style shared memory
options 	SYSVMSG			#SYSV-style message queues
options 	SYSVSEM			#SYSV-style semaphores
options 	P1003_1B		#Posix P1003_1B real-time extensions
options 	_KPOSIX_PRIORITY_SCHEDULING
options 	ICMP_BANDLIM		#Rate limit bad replies
options 	KBD_INSTALL_CDEV	# install a CDEV entry in /dev
options 	AHC_REG_PRETTY_PRINT	# Print register bitfields in debug

# output.  Adds ~128k to driver.
options 	AHD_REG_PRETTY_PRINT	# Print register bitfields in debug

# output.  Adds ~215k to driver.
device		isa
device		eisa
device		pci

# Floppy drives
device		fdc0	at isa? port IO_FD1 irq 6 drq 2
device		fd0	at fdc0 drive 0
device		fd1	at fdc0 drive 1

# ATA and ATAPI devices
device		ata0	at isa? port IO_WD1 irq 14
device		ata1	at isa? port IO_WD2 irq 15
device		ata
device		atadisk			# ATA disk drives
device		atapicd			# ATAPI CDROM drives
device		atapifd			# ATAPI floppy drives
device		atapist			# ATAPI tape drives
options 	ATA_STATIC_ID		#Static device numbering

# SCSI peripherals
device		scbus		# SCSI bus (required)
device		da		# Direct Access (disks)
device		sa		# Sequential Access (tape etc)
device		cd		# CD
device		pass		# Passthrough device (direct SCSI access)

# atkbdc0 controls both the keyboard and the PS/2 mouse
device		atkbdc0	at isa? port IO_KBD
device		atkbd0	at atkbdc? irq 1 flags 0x1
device		psm0	at atkbdc? irq 12
device		vga0	at isa?

# splash screen/screen saver
pseudo-device	splash

# syscons is the default console driver, resembling an SCO console
device		sc0	at isa? flags 0x100

# Floating point support - do not disable.
device		npx0	at nexus? port IO_NPX irq 13

# PCCARD (PCMCIA) support
device		card
device		pcic0	at isa? irq 0 port 0x3e0 iomem 0xd0000
device		pcic1	at isa? irq 0 port 0x3e2 iomem 0xd4000 disable

# Serial (COM) ports
device		sio0	at isa? port IO_COM1 flags 0x10 irq 4
device		sio1	at isa? port IO_COM2 irq 3
device		sio2	at isa? disable port IO_COM3 irq 5
device		sio3	at isa? disable port IO_COM4 irq 9

# Parallel port
device		ppc0	at isa? irq 7
device		ppbus		# Parallel port bus (required)
device		lpt		# Printer
device		plip		# TCP/IP over parallel
device		ppi		# Parallel port interface device

# PCI Ethernet NICs that use the common MII bus controller code.
# NOTE: Be sure to keep the 'device miibus' line in order to use these NICs!
device		miibus		# MII bus support

# ISA Ethernet NICs.
# 'device ed' requires 'device miibus'
device		ed0	at isa? disable port 0x280 irq 10 iomem 0xd8000
device		ex
device		ep
device		fe0	at isa? disable port 0x300

# WaveLAN/IEEE 802.11 wireless NICs. Note: the WaveLAN/IEEE really
# exists only as a PCMCIA device, so there is no ISA attachment needed
# and resources will always be dynamically assigned by the pccard code.
device		wi

# The probe order of these is presently determined by i386/isa/isa_compat.c.
device		ie0	at isa? disable port 0x300 irq 10 iomem 0xd0000
device		lnc0	at isa? disable port 0x280 irq 10 drq 0
device		cs0	at isa? disable port 0x300
device		sn0	at isa? disable port 0x300 irq 10

# Pseudo devices - the number indicates how many units to allocate.
pseudo-device	loop		# Network loopback
pseudo-device	ether		# Ethernet support
pseudo-device	sl	1	# Kernel SLIP
pseudo-device	ppp	1	# Kernel PPP
pseudo-device	tun		# Packet tunnel.
pseudo-device	pty		# Pseudo-ttys (telnet etc)
pseudo-device	md		# Memory "disks"
pseudo-device	gif		# IPv6 and IPv4 tunneling
pseudo-device	faith	1	# IPv6-to-IPv4 relaying (translation)

# The `bpf' pseudo-device enables the Berkeley Packet Filter.
# Be aware of the administrative consequences of enabling this!
pseudo-device	bpf		#Berkeley packet filter

# USB support
device		uhci		# UHCI PCI->USB interface
device		ohci		# OHCI PCI->USB interface
device		usb		# USB Bus (required)
device		ugen		# Generic
device		uhid		# "Human Interface Devices"
device		ukbd		# Keyboard
device		ulpt		# Printer
device		umass		# Disks/Mass storage - Requires scbus and da
device		ums		# Mouse
device		uscanner	# Scanners
device		urio		# Diamond Rio MP3 Player

# Sound
device pcm0 at isa? port 0x530 irq 5 drq 1 flags 0

# Power Management
device apm</pre>
```

## Programme die richtig gut laufen<
* XFCE4 - Desktop Environment
Hinweis zur Konfiguration:
.xinitrc im Home Verzeichnis der Benutzers anlegen und folgendes einfügen:
`export LC_ALL=de_DE.ISO-8859-15 export LANG=de_DE.ISO-8859-15`
`exec startxfce4`
*   Fluxbox - WindowManager
*   MC-light - Dateimanager nicht nur auf der Konsole
*   aterm - Eine Terminal Emulation als Ersatz für xfterm4
*   Abiword - Textverarbeitung
*   Gnumeric - Tabellenkalkulation (hat leider sehr viele Abhängigkeiten, braucht also Platz auf der Platte)
*   abs - Alternative zu Gnumeric. Ist leider nur in Englisch und kennt nur sein eigenes Datei Format. Aber sehr schnell.
*   Sylpheed-Claws - E-Mail Client
*   CenterICQ - Instant Messanger (geht am Besten im aterm)
*   cvsup-whithout-gui
*   portupgrade
*   libretto-config - Konfiguration des Libretto-BIOS
*   asapm - Batterie Monitor (Der Batterie Monitor von xfce4 arbeitet nur mit ACPI)
*   gnupg - The GNU Privacy Guard
*   gpa - Frontend für gnupg

## Installierte Packages
### my packages
```
pkg_add -r portupgradepkg_add -r birda
pkg_add -r sylpheed-claws
pkg_add -r centericq
pkg_add -r links (mit -g startn für GUI)
pkg_add -r xzgv (bildbetrachter)
pkg_add -r emelfm2 (file manager)
pkg_add -r libretto-config
pkg_add -r mp3blaster
pkg_add -r fluxbox-devel
pkg_add -r aterm
pkg_add -r bbapm
pkg_add -r gkrellm2pkg_add -r fluxbg (zuerst fluxbg_conf -> fluxbg)
pkg_add -r display (für das setzen mit fluxbg benötigt)
pkg_add -r fluxconf
pkg_add -r fbdesk
pkg_add -r kdebase
```
## Weiterführende Links
* [Linux and the Toshiba Libretto 100CT](http://www.lns.com/papers/libretto100/)
* [Installing Debian "Woody" Linux on the Libretto 50CT](http://www.ladle.demon.co.uk/misc/libretto-debian.html)
* [Which version on Linux on Libretto 100CT](http://www.linuxquestions.org/questions/showthread.php?s=&threadid=93403&highlight=libretto)
* [Install on Libretto (No Bootable CD Drive)](http://www.linuxquestions.org/questions/showthread.php?s=&forumid=1&threadid=235141)
* [Phil's Toshiba Libretto Seiten](http://www.sumesgutner.de/philip/libretto/index.htm)
* [Libretto Subnotebook-Forum](http://nightlife-sendenhorst.de/Toshiba/Forum/index.php)