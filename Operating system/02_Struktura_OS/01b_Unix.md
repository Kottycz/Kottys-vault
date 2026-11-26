---
aliases: [UNIX, UNIX a Linux, Struktura UNIX]
tags: [os]
---

## UNIX a UNIX LIKE SYSTÉMY

Většina UNIX a UNIX LIKE systémů má podobnou strukturu (kromě těch upravených pro RealTimový provoz – RT).

### Základní vlastnosti

- od začátku (1970) **víceprocesorové, víceuživatelské, víceúlohové, síťové**
- s tím se počítalo už při návrhu → strukturu nebylo potřeba desítky let výrazně měnit
- vzor pro návrh **Windows NT**

### Jádro

- běží v privilegovaném režimu, je to ==jediný soubor== s jediným souvislým adresovým prostorem → **monolitické** (i když má bohatou vnitřní strukturu)
- Linux: `/boot/vmlinuz`
- dvě části: **HAL** (závislý na hardwaru) a **kernel** (nezávislý na hardwaru)

#### HAL

- **Hardware Abstraction Layer** – základní rozhraní k zařízením, používají ho i ovladače
- skrývá technické detaily zařízení různých tříd
- načítá ovladače, vytváří a ruší přípojné body blokových zařízení, provozuje abstraktní model hardwaru

#### Ovladače

- důležité moduly jádra: ovladače **znakových, blokových, síťových** zařízení a další
- i **souborové systémy** jsou implementované jako ovladače

### Souborové systémy

- souborový systém = rozhraní mezi ovladačem paměťového média a vyššími vrstvami jádra
- ==„všechno je soubor“== – i informace o stavu systému a jádra v paměti se zpřístupňují jako soubory (Linux: `/proc`)
- **virtuální souborové systémy** – nepatří k žádnému médiu, ale zacházíme s nimi jako se soubory

#### VFS

- **Virtual File System** – nejdůležitější souborový systém
- jednotné rozhraní pro přístup k různým souborovým systémům
- všechny je sdružuje do **jednoho stromu** – souborový systém se zpřístupní připojením (mount) na určené místo

#### FUSE

- **FileSystem in User Space** – souborové systémy běží v uživatelském prostoru (běžné musí být v jádru)
- dvě části: **modul FUSE** v jádru (společný pro všechny) + horní část v uživatelském režimu, která ho využívá

### Síť a podsystémy

- **síťové protokolové zásobníky** (TCP/IP) jsou součástí jádra
- **podsystémy** se specifickou funkcí: šifrovací, multimediální, IPC, bezpečnostní moduly…

### Systémová volání a knihovny

- **rozhraní systémových volání** = rozhraní mezi jádrem a vším, co ovlivní uživatel (programy, příkazy shellu, skripty)
- systémová volání = funkce pro komunikaci s jádrem; chrání bezpečnost a stabilitu – aplikace nesmí přímo do jádra
- volají se přes **knihovny** s API funkcemi:
  - Linux: **glibc** (GNU C Library)
  - UNIX: **libc**
- procesy pošlou požadavek knihovně, ta ho předá rozhraní systémových volání

### Shell

- **Shell** = textové rozhraní s uživatelem (příkazy → textové výpisy); v Linuxu většinou **Bash** (Bourne Again Shell)
- unixové systémy mají i propracované grafické rozhraní, obvykle na **X WINDOW**

![[298f6c92b5c164b55f990a8d0f915b29f09896f4e26d4367e9934851187fe18b.png]]

### STANDARDY

- **POSIX** – Portable Operating System Interface → UNIX LIKE
- **SUS** – Single UNIX Specification → UNIX CERTIFIED

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
| checksumy dat | | | | | x | x |
| copy-on-write (CoW) | | | | | x | x |
| self-healing | | | | | x | x* |
| online zvětšování/zmenšování | | x | | x** | x | x |
| symbolické odkazy | | x | x | x | x | x |
| hard linky | | x | x | x | x | x |
| soubory >4 GB | | x | x | x | x | x |
| nativně ve Windows | x | x | | | | |
| nativně v Linuxu | x | x*** | x | x | x**** | x |
| nativně v macOS | x | čtení | | | | |

- \* **BTRFS** self-healing jen s redundancí (RAID1/10); RAID5/6 je stále problematický
- \*\* **EXT4** zvětšuje online, zmenšuje jen offline
- \*\*\* **NTFS** v Linuxu přes ntfs3 (jádro) nebo ntfs-3g
- \*\*\*\* **ZFS** není v jádře kvůli licenci (CDDL), instaluje se jako modul (OpenZFS)
- **BTRFS** šifrování nativně nemá, používá se LUKS pod ním

---

**Struktura OS:** [[01_STRUKTURA_OPERAČNÍCH_SYSTÉMŮ|Architektury OS]] · [[01a_Windows|Windows]] · [[01b_Unix|UNIX]] · [[01c_Linux|Linux]] · [[01d_Apple|Apple]] · [[01e_Android|Android]]
