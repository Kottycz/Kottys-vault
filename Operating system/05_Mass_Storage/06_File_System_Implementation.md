---
aliases: [File-System Implementation, Implementace souborového systému, MBR, GPT]
---

# Implementace souborového systému

## Struktura souborového systému (vrstvy)

1. **I/O control** – ovladače a obsluha přerušení; překládá „přines blok 123“ na instrukce řadiče
2. **Basic file system** – obecné příkazy ovladači, buffery a [[cache]]
3. **Logická vrstva** – **metadata** (vše kromě obsahu souborů) a adresáře přes **[[FCB]]**

Vrstvy omezují duplicitu kódu, ale přidávají režii.

**Běžné FS:** UFS (UNIX), FAT/FAT32/NTFS (Windows), ext3/ext4 (Linux), ISO 9660 (CD), FUSE (v uživatelském režimu), Google File System.

## FCB (File Control Block)

Metadata jednoho souboru – vlastník, oprávnění, umístění obsahu. V UNIXu **inode**.

## On-disk a in-memory struktury

**Na disku:**

- **boot control block** (na svazek) – info pro zavedení OS (UFS boot block, NTFS partition boot sector)
- **volume control block** (na svazek) – počet a velikost bloků, volné bloky (UFS superblock, NTFS master file table)
- **adresářová struktura** – jména souborů + čísla inode
- **FCB** pro každý soubor

**V paměti:**

- **mount table** – připojené svazky
- **cache adresářů** – nedávno použité adresáře
- **systémová open-file table** – kopie FCB otevřených souborů
- **per-process open-file table** – ukazatel do systémové tabulky + info procesu
- **buffery** – bloky při čtení a zápisu

**Vytvoření a otevření souboru:**

1. `create()` – nový FCB, aktualizace adresáře
2. `open()` – nejdřív systémová open-file table (soubor už může mít otevřený jiný proces); jinak hledání v adresáři, FCB do systémové tabulky a záznam do per-process tabulky
3. `open()` vrátí **file descriptor / handle** – používá se pro další operace, adresář se znovu neprohledává

## Oddíly a mountování

- **raw oddíl** – bez souborového systému (swap, některé databáze, metadata RAID)
- **„cooked“ oddíl** – se souborovým systémem
- **boot partition** – zavaděč v pevném formátu (FS ještě není načtený)
- **root partition** – jádro OS, mountuje se při startu

### MBR (Master Boot Record)

Na začátku disku (LBA sektor 0), dvě části:

- **tabulka oddílů (MPT)** – max. **4 primární oddíly**; jeden může být **extended** s libovolným počtem logických oddílů
- **zavaděč** – BIOS ho nahraje a spustí, ten spustí boot sektor aktivního oddílu
- **limit:** 32bitová adresace → disky max **2 TiB**

### GPT (GUID Partition Table)

- součást **UEFI**, nahrazuje MBR
- disky nad 2 TiB, prakticky neomezený počet oddílů
- převod z MBR je snadný, pokud je první oddíl zarovnaný (od Vista na 1 MiB)

## Virtual File System (VFS)

Jednotné rozhraní pro víc typů FS najednou (lokální i síťové):

1. **rozhraní systémových volání** (`open, read, write, close`)
2. **VFS** – odděluje obecné operace od implementace; používá **vnode** (jedinečný v celé síti, ne jen v jednom FS) → stejný přístup k lokálním i **[[NFS]]** souborům
3. **konkrétní implementace** FS nebo síťového protokolu

Linux VFS má 4 objekty: **inode** (soubor), **file** (otevřený soubor), **superblock** (celý FS), **dentry** (položka adresáře).

## Implementace adresáře

- **lineární seznam** – jednoduchý, ale pomalé hledání (setříděný → binární hledání, ale složitější vkládání)
- **hašovací tabulka** – rychlé hledání; problém s pevnou velikostí a kolizemi (řetězení)

## Metody alokace místa na disku

### Souvislá alokace (Contiguous)

- soubor = **souvislý úsek** (začátek + délka); blok i = b+i
- **+** málo seeků, sekvenční i přímý přístup
- **−** **externí fragmentace** (first/best/worst fit jako u [[02_Hlavni_pamet|paměti]]), velikost se musí znát předem, kompakce je drahá

### Spojová alokace (Linked)

- soubor = [[spojový seznam]] bloků kdekoli na disku; adresář má ukazatel na první a poslední
- **+** žádná externí fragmentace, velikost netřeba znát
- **−** rozumné jen pro **sekvenční přístup** (k i-tému bloku přes i−1 předchozích), poškozený ukazatel = ztráta zbytku, místo na ukazatele (řeší **clustery**)
- **FAT** – varianta z MS-DOS: tabulka indexovaná číslem bloku, záznam ukazuje na další blok (0 = volný, speciální hodnota = konec); když je v cache, je i přímý přístup rychlý

### Indexovaná alokace (Indexed)

- každý soubor má **index blok** – i-tý záznam = adresa i-tého bloku
- **+** přímý přístup, bez externí fragmentace
- **−** u malých souborů plýtvá místem
- velké soubory: **spojované** index bloky, **víceúrovňový** index, nebo **kombinace (UNIX [[i-node|inode]])** – ~12 přímých ukazatelů + single/double/triple indirect

| | Souvislá | Spojová | Indexovaná |
| :-- | :-- | :-- | :-- |
| sekvenční přístup | rychlý | rychlý | podle cache indexu |
| přímý přístup | rychlý (1 čtení) | pomalý (i čtení) | rychlý, je-li index v paměti |
| externí fragmentace | ano | ne | ne |

Některé systémy kombinují – malé soubory souvisle, velké indexovaně.

## Správa volného místa

- **bitová mapa** – 1 bit na blok (1 = volný); rychlé hledání prvního volného bloku
- **spojový seznam volných bloků** – stačí najít jeden volný, celý se neprochází; FAT to řeší přímo v tabulce (0 = volný)

## Obnova po havárii (Recovery)

- **kontrola konzistence** (`fsck`) – porovná adresáře s daty na disku a opraví; u velkých disků minuty až hodiny
- **žurnálovací FS** – viz [[žurnálování]]; změny metadat jdou nejdřív do **logu**, pak do struktur. Po havárii se dokončí potvrzené (committed) transakce a nepotvrzené se vrátí → mnohem rychlejší než fsck
- **zálohování:**
  - den 1 **plná záloha**
  - další dny **přírůstková** (jen změny od poslední zálohy)
  - obnova = plná + postupně přírůstkové

## NFS (Network File System)

Sdílení souborů mezi stanicemi na principu **klient-server** – stroj může být klient i server zároveň, týká se jen zúčastněných strojů.

**Souvisí:** [[FCB]], [[i-node]], [[žurnálování]], [[cache]], [[spojový seznam]], [[hašovací tabulka]], [[04_File_Concept_Access]], [[05_Directory_Structures]]
