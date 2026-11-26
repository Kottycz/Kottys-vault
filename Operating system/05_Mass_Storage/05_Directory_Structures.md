---
aliases: [Directory Structure, Adresářová struktura, File Sharing, File System Mounting, Protection]
---

# Adresářové struktury, mountování, sdílení a ochrana

## Operace s adresářem

Hledání, vytvoření a smazání souboru, výpis obsahu, přejmenování, průchod celou strukturou (záloha).

## Typy adresářové struktury

### Jednoúrovňový adresář (Single-Level)

- všechny soubory v jednom adresáři
- jednoduché, ale **jména musí být unikátní** v celém systému → nepraktické

### Dvouúrovňový adresář (Two-Level)

- každý uživatel má **UFD** (User File Directory), jejich index je **MFD** (Master File Directory)
- jména unikátní jen v rámci UFD, ale uživatelé jsou **izolovaní** – k cizímu souboru přes **cestu** `/uzivatel/soubor`
- **search path** – kde se hledá spustitelný soubor (vlastní UFD, pak systémový adresář)

### Stromová struktura (Tree-Structured)

- libovolná hloubka, vlastní podadresáře, **kořenový adresář**, každý soubor má unikátní cestu
- adresář je speciální soubor (bit odliší soubor a podadresář)
- každý proces má **aktuální adresář**; **absolutní** cesta od kořene, **relativní** od aktuálního adresáře
- mazání neprázdného adresáře: zakázat, nebo smazat rekurzivně (`rm -r`)

### Acyklický graf (Acyclic-Graph)

- **sdílení** souborů a podadresářů mezi víc adresáři (týmová práce)
- sdílený soubor **není kopie** – existuje jen jeden, změny vidí všichni
- implementace: **link** (záznam s cestou ke skutečnému souboru) nebo **duplicitní záznam** (hůř se udržuje konzistentní)
- mazání: hardlinky mají **počítadlo referencí** – soubor se smaže až při 0; u symbolického odkazu zůstane „visící“ odkaz (dangling link), který prostě selže

### Obecný graf (General Graph)

- odkazy vytvoří **cyklus** → riziko nekonečné smyčky a počítadlo referencí nemusí klesnout na 0
- řešení: **garbage collection** (drahé), nebo **při procházení linky přeskakovat**

## Mountování souborového systému

- FS se před použitím musí **připojit (mount)**: zařízení + **mount point** (obvykle prázdný adresář)
- OS ověří, že zařízení má platný FS, a zapíše si, kde je připojený
- **UNIX/Linux** – kamkoli do stromu
- **Windows** – **písmena disků** (C:, D:), novější i do složky
- **macOS** – automaticky pod `/Volumes`

## Sdílení souborů (File Sharing)

- úrovně vlastnictví: **owner** (mění práva), **group**, **universe** (všichni ostatní)
- **vzdálené FS:** ruční přenos (FTP), **DFS** – vzdálené složky jako lokální (NFS, CIFS), WWW
- **klient-server:** server zpřístupní soubory, klient přes síť
  - **NFS** ověřuje jen podle identity klienta (ID musí sedět, nešifrované, snadno zneužitelné)
  - bezpečněji: šifrované klíče, **LDAP** – standard pro správu identit, stojí na něm i **Active Directory**
- **distribuované informační systémy:**
  - **DNS** – překlad jmen na adresy
  - **NIS** („yellow pages“) – jména a hesla centrálně, nešifrované, zastaralé
  - **Active Directory / LDAP** – bezpečné jednotné přihlášení (single sign-on)

## Ochrana (Protection)

**Řízené operace:** Read, Write, Execute, Append, Delete, List (+ odvozené: přejmenování, kopírování).

**Řízení přístupu:**

- **ACL** (Access Control List) – seznam uživatelů a jejich práv; flexibilní, ale může být dlouhý
- **owner/group/universe** – UNIX **rwx** (3 bity × 3 kategorie = 9 bitů)
- **kombinace** (Solaris) – rwx + volitelné ACL

**Jiné přístupy:**

- heslo na soubor/adresář – nepraktické (moc hesel, nebo „všechno, nebo nic“)
- chránit se musí i operace s adresáři (vytvoření, smazání, výpis), nejen soubory

**Souvisí:** [[04_File_Concept_Access]], [[06_File_System_Implementation]], [[proces]]
