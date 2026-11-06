---
aliases: [Linux, Architektura Linux, Jádro Linux]
tags: [os]
---

# LINUX

## JÁDRO LINUX

Obrázek je cíleně vytvořen tak, aby ve sloupcích byly nad sebou ty součásti, které spolu významově souvisejí, včetně vazby na konkrétní kus hardwaru. Některé součásti souvisejí se dvěma hardwarovými komponentami, například **SWAP** (odkládací oblast) souvisí s operační pamětí (protože stránky z ní se odkládají na disk) a zároveň s paměťovými médii (protože na ta se odkládá). Síťová úložiště souvisejí se sítí (protože se k nim přistupuje přes síť) a zároveň s paměťovými médii (protože z nich se čte a na ně se zapisuje).

Modely zařízení se vztahují jak k síťovým rozhraním, tak i k dalším I/O zařízením, protože jejich strukturu popisují.

![[df9c8730a6735815966377c53dcec7d0a11a7b16995636f952de976d42fe71b4.png]]

### CHARAKTERISTIKA

- **UNIX LIKE OS**

#### GNU/GPL licence

- Uveď co tato licence umožňuje

- ==LINUX== = Jádro OS
- ==GNU/LINUX== = celý OS = jádro + všechno "okolo"

#### LINUS TORVALDS

- 21 let - studentský projekt

#### VLASTNOSTI

##### LINUX tvoří malé, nenáročné programy a příkazy

- Složitější úlohy se poskládají z více jednoduchých

- Propracovaná komunikace mezi procesy
- Všechno je "SOUBOR"
- Běží na jakémkoliv HW
- Nenáročný na zdroje
- Stabilita

#### ZDROJE

- http://www.linux.org
- http://www.linux.cz

### ARCHITEKTURA LINUX DISTRIBUCE

#### LINUXOVÁ DISTRIBUCE =

- **LINUX** = jádro (KERNEL) operačního systému

##### INSTALÁTOR

- Instalační rutina, průvodce instalací

- **DETEKTOR HW**
- **SYSTÉMOVÉ KNIHOVNY**
- **KONFIGURAČNÍ NÁSTROJE**

##### GRAFICKÉ PROSTŘEDÍ

###### DESKTOP ENVIRONMENT

**X WINDOW**

Doplňte co je X WINDOW a jakou funkcionalitu zajišťuje

**WIDGET TOOLKIT**

- Doplňte co je WIDGET

**WINDOW MANAGER**

**Window Maker**

- http://www.windowmaker.info/

**AfterStep**

- http://www.afterstep.org/

**FluxBox**

- http://www.fluxbox.org/

**OpenBox**

- http://icculus.org/openbox/index.php/Main Page

**Xmonad**

- http://xmonad.org/

**IceWM**

- http://www.icewm.org/

**fvwm**

- http://www.fvwm.org/

**SawFish**

- http://sawfish.wikia.com/wiki/Main Page

Vyberte si některého správce oken a doplňte jeho stručnou charakteristiku

**Přehled Desktopových prostředí**

**CDE**

- http://www.opengroup.org/tech/desktop/cde/

**KDE**

- http://www.kde.org/

**GNOME**

- http://www.gnome.org/

**CINNAMON**

- http://developer.linuxmint.com/reference/index.html
- http://www.zdnet.com/article/how-tocustomise-your-linux-desktop-cinnamon/

**MATE**

- http://mate-desktop.com/

**LXDE**

- ttp://lxde.org/

**ENLIGHTMENT**

- ttp://www.enlightenment.org/

**XFCE**

- http://www.xfce.org,

**3D PROSTŘEDÍ**

**Compiz Fusion**

- https://www.youtube.com/watch?v=4QokOwvPxrE
- http://wiki.compiz-fusion.org/
- http://wiki.compiz-fusion.org/

**Looking Glass**

- https://www.youtube.com/watch?v=EjQ4Nza34ak
- http://www.sun.com/software/looking glass/
- https://lg3d-livecd.dev.java.net/Web-Site/Welcome.html

**Croquet**

- http://www.opencroquet.org/
- http://www.linuxexpres.cz/modules/marwel/index.php?article=1856
- http://www.root.cz/serialy/squeak-navrat-do-budoucnosti/
- http://www.squeak.org/, http://laptop.org/en/

Ke každému desktopovému prostředí doplňte screenshoty pr ilustraci jeho vzhledu

Vyberte si jedno z uvedených desktopových prostředí a doplňte jeho stručnou charakteristiku

###### DALŠÍ ZDROJE

- http://xwinman.org/
- http://en.wikipedia.org/wiki/Comparison of X window managers
- http://en.wikipedia.org/wiki/Comparison of X Window System desktop environments

- APLIKACE

##### DOKUMENTACE

- Linux Dokumentační Projekt
- HOW TO
- Manuálové stránky

Doplňte internetové odkazy na výše uvedenou dokumentaci

#### NEJZNÁMĚJŠÍ DISTRIBUCE

##### Komerční

- RedHat
- RedHat Enterprice Server
- SuSe

##### Komunitní

- Debian
- Ubuntu
- Fedora
- OpenSuSe
- Mandriva
- Mint
- SlackWare
- Gentoo
- RT Linux
- PartedMagic

Ke každé z uvedených linuxových distribucí doplňte: 0. Charakteristiku distribuce 1. Odkaz na původní a českou verzi stránek distribuce 2. Aktuální stabilní verze 3. Podporované HW Platformy 4. Používaná grafická prostředí 5. Typ instalačních balíčů (DEB, RPM, SRT, ...) 6. Odkaz na ISO obraz instalačního CD 7. Odkaz na uživatelskou dokumentaci 8. Odkaz na Diskusní fórum

#### ZDROJE

##### www stránky jednotlivých distribucí

- www.debian.org
- www.debian.cz
- www.ubuntu.cz

- http://distrowatch.com
- http://livecdlist.com/

- Zde uveďte aktuální stabilní verzi jádra LINUX

### SOUBOROVÝ SYSTÉM

Vyjmenujte souborové systémy používané v distribucích UBUNTU, DEBIAN, MINT

#### Správce souborů

Vložte Printscreen prostředí správce souborů v UBUNTU Vložte Printscreen prostředí správce souborů v DEBIAN Vložte Printscreen prostředí správce souborů v MINT

#### Sooborová struktura

##### VŠECHNO JE SOUBOR

- SOUBOR
- ADRESÁŘ
- BD, CD, DVD
- PRINTER
- SCANNER
- ZAŘÍZENÍ
- ATD

##### STROMOVÁ STRUKTURA

###### ADRESÁŘ

- JE SOUBOR Se seznamem svého obsahu

###### PODADRESÁŘ

- JE SOUBOR Se seznamem svého obsahu

###### SOUBOR

- JE SOUBOR Se svým obsahem

#### TYPY SOUBOROVÝCH SYSTÉMŮ

##### EXTn

- EXT2
- EXT3
- EXT4

- REISERFS
- XFS
- JFS
- NFS
- SMB

Doplňte krátkou charakteristiku každého uvedeného FS

### ZKOUMÁME SOUBOROVÝ SYSTÉM

#### NÁZVY SOUBORŮ

- Délka názvu obvykle do **255 znaků**
- Mohou a nemusí mít příponu
- Přípona může být jakkoliv dlouhá
- Přípona je součástí názvu včetně oddělující tečky
- Spustitelné soubory příponu nemají
- Název skrytých souborů začíná **TEČKOU**

##### Názvy adresářů končí ".d"

- Název.d
- Home.d
- etc.d

#### /

##### /bin: Essential user command binaries (for use by all users)

Základní příkazy pro textový režim (jejich spustitelné soubory) pro různé účely (název bin je od „binary"), mohou být používány i krátce po startu systému, tyto příkazy může obvykle spouštět i běžný uživatel, je tu například **cp** pro kopírování (ve Windows máme copy) nebo **ls** pro výpis obsahu adresáře (ve Windows máme dir)

##### /boot : Static files of the boot loader

- Soubory zaváděče operačního systému

##### /dev : Device files

Zařízení - soubory reprezentující zařízení a přístupové body k nim = realizují nízkoúrovňovou komunikaci se zařízením, které reprezentují.

##### /etc : Host-specific system configuration

Konfigurační soubory pro systém i mnohé aplikace (aplikace si zde pro vlastní potřeby vytvářejí podadresáře)

##### /home : User home directories

- Radim
- Petra
- Martin
- Hana
- Domovské adresáře uživatelů

##### /lib : Essential shared libraries and kernel modules

Sdílené knihovny využívané při startu systému nebo pro programy z /bin a /sbin, v podadresáři modules najdeme moduly jádra

##### /media : Mount point for removeable media

- usb
- diskC
- eth0

- /mnt : Mount point for a temporarily mounted
- /opt : Add-on application software packages

##### /root : Home directory for the root user

- Domovský adresář uživatele root (správce systému)

##### /sbin : System binaries

Různé utility pro správu systému vyžadující pro své spuštění oprávnění **superuser**

##### /proc : Kernel and process information virtual filesystem

Najdeme zde běhové informace o systému a procesech, tj. informace, které se dynamicky mění za běhu systému (proto běhové)

- /tmp : Temporary files

##### /usr

Statické (málo se měnící) části instalace aplikací, například spustitelné soubory, knihovny, konfigurační soubory, případně zdrojové soubory, dokumentace, nápověda,

##### /var

Často se měnící části instalace aplikací (variable), například logy, dočasné soubory, tiskové fronty apod.

/proc : Kernel and process information virtual filesystem

#### Odkazování na některé adresáře

##### /

- Kořenový adresář

##### .

- Aktuální adreář

##### ..

- Nadřazený adresář

##### ~

#### ODKAZY NA SOUBOR

- **HARDLINK**
- **SOFTLINK**

Dopňte, co j e HARDLINK, CO JE SOFTLINK a jaký je mezi nimi rozdíl

- http://www.pathname.com/fhs/pub/fhs-2.3.pdf
- http://www.pathname.com/fhs/

---

**Struktura OS:** [[01_STRUKTURA_OPERAČNÍCH_SYSTÉMŮ (1)|Architektury OS]] · [[01a_Windows|Windows]] · [[01b_Unix|UNIX]] · [[01c_Linux|Linux]] · [[01d_Apple|Apple]] · [[01e_Android|Android]]
