---
aliases: [UNIX, UNIX a Linux, Struktura UNIX]
tags: [os]
---

## UNIX a UNIX LIKE SYSTÉMY

Většina UNIX a UNIX LIKE systémů má podobnou strukturu (kromně těch upravených pro RealTimový provoz - RT).

### Základní vlastnosti

UNIXové systémy jsou **víceprocesorové, víceuživatelské, víceúlohové, síťové** systémy od svého počátku (1970). Na to byl brán zřetel už při navrhování těchto systému a proto za dlouhá desetiletí jejich existence nebylo potřeba jejich strukturu výrazněji měnit. Staly se taky vzorem pro návrh struktury WINDOWS NT systémů.

### Jádro

Jádro běží v privilegovaném režimu, je tvořeno ==jediným souborem== a využívá jediný souvislý adresový prostor, proto je nazýváno **monolitické**, i když má bohatou vnitřní strukturu. U linuxu je to soubor `/boot/vmlinuz`.

Jádro systému se skládá ze dvou oddělených částí. **HAL** (Hardware Abstraction Layer) závislé na hardware a **kernelu** nezávislého na hardware. Jádro je typicky monolitické, načítá se z jednoho souboru do jednoho souvislého adresního prostoru.

#### HAL

Vrstva **HAL** (Hardware Abstraction Layer) slouží jako základní rozhraní k zařízením, které je také využíváno ovladači ke komunikaci se zařízeními.

- Hlavním úkolem HAL je skrýt technické detaily zařízení patřících do různých tříd (skupin s charakteristickými vlastnostmi).
- HAL zajišťuje načítání ovladačů, vytváření a odstraňování přípojných bodů pro bloková zařízení a také provozování abstraktního modelu hardware.

#### Ovladače

Důležitými moduly jádra jsou **ovladače**. Existují ovladače znakových zařízení, blokových zařízení, síťových zařízení a další specializované ovladače. Také souborové systémy jsou implementovány jako ovladače.

### Souborové systémy

**Souborový systém** je v Unixových systémech vlastně rozhraní mezi ovladačem vnějšího paměťového média a vyššími vrstvami jádra.

V UNIXu platí, že ==„všechno je soubor“== a jako souborový systém je implementován například přístup k informacím o stavu systému, stavu jádra, konfiguraci, které běží v paměti a nejedná se o žádný soubor (v linuxu například adresář proc).

Souborové systémy, které nenáležejí k žádnému konkrétnímu paměťovému médiu, ale přesto s nimi zacházíme, jako by se jednalo o soubory a systémy souborů nazýváme **virtuální souborové systémy**.

#### VFS

**VFS** (Virtual File System) je nejdůležitějším souborovým systémem. Představuje jednotné rozhraní pro podobný přístup k různým souborovým systémům. Všechny souborové systémy sdružuje v jediné stromové struktuře. Pokud uživatel chce s konkrétním souborovým systémem pracovat, připojí ho na stanovené místo do této struktury a tím ho zpřístupní.

#### FUSE

**FUSE** (FileSystem in User Space) je mechanismus, který umožňuje běh souborových systémů v uživatelském prostoru (běžné souborové systémy musí být součástí jádra).

Spočívá v rozdělení souborového systému do dvou částí, spodní část – modul FUSE – je pro všechny souborové systémy tohoto typu společná a běží v režimu jádra. Horní část běží v uživatelském režimu a využívá služeb modulu FUSE.

### Síť a podsystémy

**Síťové protokolové zásobníky** (např. TCP/IP) jsou implementovány jako součást jádra.

**Podsystémů** existuje poměrně hodně a každý má svou specifickou funkci. Například šifrovací subsystém, multimediální subsystém, IPC (inter proces communication) subsystém, bezpečnostní moduly, atd.

### Systémová volání a knihovny

**Rozhraní systémových volání** je rozhraní mezi jádrem a čímkoli, co může přímo ovlivnit uživatel (programy, příkazy shellu, skripty).

S touto vrstvou lze komunikovat přes knihovny obsahující definice API funkcí, která mohou generovat systémová volání. Hlavní úlohou je zajištění bezpečnosti a stability systému a znemožnění zásahu uživatele (aplikace bežící v kontextu uživatele) do jádra. Systémová volání jsou vlastně funkce, kterými lze komunikovat s jádrem.

V systému je velké množství knihoven, z nicž v LINUXU je nejdůležitější knihovna **glibc** (GNU C LINRARY) v UNIX systémech je to **libc**.

Tato knihovna zprostředkovává komunikaci procesů z uživatelského prostoru s rozhraním systémových volání (procesy zasílají systémová volání této knihovně).

### Shell

**Shell** je rozhraní pro komunikaci s uživatelem. Unixové systémy obvykle nabízejí více druhů Shellů. V Linuxu máme většinou **Bash** (Bourne Again Shell).

Komunikace probíhá v textové formě. Uživatel zadává příkazy, systém reaguje textovými výpisy), ale současně UNIX systémy mají také propracované grafické rozhraní (obvykle založené na **X WINDOW**).

![[298f6c92b5c164b55f990a8d0f915b29f09896f4e26d4367e9934851187fe18b.png]]

### STANDARDY

#### POSIX

- **Portable Operating System Interface**
- UNIX LIKE

#### SUS

- **SINGLE UNIX SPECIFICATION**
- UNIX CERTIFYIED

### Porovnání souborových systémů

| | FAT32 | NTFS | EXT2 | EXT4 | ZFS | BTRFS |
|---|---|---|---|---|---|---|
| file handling | x | x | x | x | x | x |
| [[žurnálování]] | | x | | x | x | x |
| komprese | | x | | | x | x |
| šifrování | | x | | x | x | |
| oprávnění | | x | x | x | x | x |
| kvóty | | x | x | x | x | x |
| snapshoty | | | | | x | x |
| deduplikace | | | | | x | x |
| [[RAID]] | | | | | x | x |
| checksumy dat (ochrana proti poškození) | | | | | x | x |
| copy-on-write (CoW) | | | | | x | x |
| self-healing | | | | | x | x* |
| online zvětšování/zmenšování | | x | | x** | x | x |
| symbolické odkazy | | x | x | x | x | x |
| hard linky | | x | x | x | x | x |
| podpora souborů >4 GB | | x | x | x | x | x |
| nativní podpora ve Windows | x | x | | | | |
| nativní podpora v Linuxu | x | x*** | x | x | x**** | x |
| nativní podpora v macOS | x | čtení | | | | |

- \* **BTRFS** umí self-healing jen s redundantním profilem (RAID1/10 apod.); u RAID5/6 je stále považován za problematický
- \*\* **EXT4** umí online zvětšování, zmenšování jen offline
- \*\*\* **NTFS** v Linuxu funguje přes ovladač ntfs3 (jádro) nebo ntfs-3g
- \*\*\*\* **ZFS** není v Linuxovém jádře kvůli licenci (CDDL), instaluje se jako modul (OpenZFS)
- **šifrování u BTRFS:** nativně nemá, používá se LUKS pod ním


---

**Struktura OS:** [[01_STRUKTURA_OPERAČNÍCH_SYSTÉMŮ (1)|Architektury OS]] · [[01a_Windows|Windows]] · [[01b_Unix|UNIX]] · [[01c_Linux|Linux]] · [[01d_Apple|Apple]] · [[01e_Android|Android]]
