# [Co má být na konci projektu a jak to vypadá?]

> Verze: 2026-10-03

### 0. Připravené servery
Než vznikne cokoliv další, oba servery (**SRV1-DC**, **SRV2-FS**) mají hotový [[Modul 0 Příprava/__zadani|Modul 0 — Příprava]]: nainstalovaný Windows Server 2025 Datacenter (Desktop Experience), správný hostname, statickou IP, účet `Administrator`/`Pa55w.rd` a lokalizaci (anglické rozhraní, česká regionální nastavení a klávesnice, časové pásmo Praha).

### 1. Doménová infrastruktura a centrální identita
Na konci projektu budete mít funkční **doménu Active Directory** `prijmeni.cyberschool.internal` (za `prijmeni` vaše příjmení, např. `novak.cyberschool.internal`), spravovanou řadičem domény **SRV1-DC** (Windows Server), pro školu CyberSchool se čtyřmi obory (osmileté a čtyřleté gymnázium, elektrotechnika, informatika).

- Všichni uživatelé školy (učitelé, žáci i ostatní zaměstnanci) se přihlašují **jedním účtem** na libovolném klientském počítači v doméně, podle schématu `jmeno.student@prijmeni.cyberschool.internal` / `jmeno.teacher@prijmeni.cyberschool.internal` / `jmeno.zamestnanec@prijmeni.cyberschool.internal` (`jmeno` = křestní jméno bez diakritiky). Ve vzorovém postupu jde o 6 žáků (po dvou z osmiletého a čtyřletého gymnázia, po jednom z elektrotechniky a informatiky), 2 učitele a 2 zaměstnance.
- Uživatelé jsou rozdělení do organizační struktury OU (`Skola\Zamestnanci\{Ucitele,Vedeni,THP}`, `Skola\Studenti\{Gymnazium-8lete,Gymnazium-4lete,Elektrotechnika,Informatika}`, `Skola\Pocitace\...`), s odpovídajícími bezpečnostními skupinami (globální skupiny `GG_*` podle role a oboru — např. `GG_Studenti_IT` vnořená do `GG_Studenti`, doménové lokální skupiny `DL_*` pro přístup ke zdrojům — princip AGDLP, podrobně v Modulu 4).
- Klientský počítač **PC1-WIN** je členem domény a přihlásit se na něm může kterýkoliv platný uživatel.
- Administrace probíhá výhradně přes vestavěný účet `Administrator` — žádný personalizovaný administrátorský účet v tomto vzorovém postupu neexistuje (viz [[00-pribeh-skoly|příběh školy]]).

### 2. Síťové služby (DHCP a DNS)
Síť `192.168.200.0/24` (VLAN 200) je plně automatizovaná.

- Server **SRV1-DC** přiděluje klientům IP adresy, masku, bránu a DNS server automaticky přes **DHCP** — žádný klientský počítač nemá IP nastavenou ručně.
- **DNS server** na SRV1-DC spolehlivě překládá jména všech serverů a klientů v doméně `prijmeni.cyberschool.internal` oběma směry (dopředná i reverzní zóna).

### 3. Řízení pomocí zásad skupiny (Group Policy)
Chování počítačů a účtů se řídí centrálně, ne ručním nastavováním na každém stroji.

- Žáci mají omezená oprávnění (nemohou měnit systémová nastavení, spouštět nepovolené nástroje).
- Učitelé mají odlišná pravidla než žáci (větší volnost, jiné výchozí nastavení plochy).
- Tiskárny se nasazují uživatelům automaticky přes GPO, bez ruční instalace na každém PC.

### 4. Úložiště a souborové služby
Škola má spolehlivé a strukturované úložiště nezávislé na jediném disku.

- Server **SRV2-FS** (Windows Server s Desktop Experience, stejně jako SRV1-DC) má nakonfigurované **Storage Spaces** — datový svazek `D:\Data` přežije výpadek jednoho fyzického disku.
- Existuje adresářová struktura odpovídající reálnému provozu školy — domovské složky žáků po oborech (`Studenti\<obor>\<uzivatel>`) a zaměstnanců (`Zamestnanci\<uzivatel>`), sdílené složky předmětových komisí (`Predmetove-komise\<komise>`), a dále `Vedeni`, `Smernice`, `Verejne`, `THP` — se správně nastavenými NTFS a sdílenými oprávněními přes doménové lokální skupiny (`DL_*`).
- Domovské adresáře (`Home folders`) uživatelů jsou přesměrované na SRV2-FS.

### 5. Vzdálený přístup k souborům (FTP)
Škola umožňuje bezpečný přístup k datům i mimo lokální síť.

- Na SRV2-FS běží **FTP server** se strukturou `Studenti\Odevzdavani` (odevzdávání úkolů) a `Ucitele\Podklady` (materiály ke stažení) a oprávněními podle role uživatele.
- Přenos je zabezpečený (FTPS), ne jen prostý FTP.

### 6. Tiskové služby
Sborovna a obě učebny (učebna informatiky pro průmyslovku, gymnaziální učebna) mají centrálně spravovaný tisk.

- Na SRV2-FS je nainstalována role **Print and Document Services**.
- Tři sdílené tiskárny jsou nasazené uživatelům podle role a oboru (učitelé → sborovna, elektrotechnika a informatika → učebna informatiky, gymnázium → gymnaziální učebna) přes Group Policy, bez nutnosti ruční instalace na klientech.

### 7. Dokumentace
Celý postup výstavby je zdokumentovaný v `.md` souborech (Obsidian) — pro každý modul existuje popis cílového stavu, postup řešení a návod, jak ověřit, že modul funguje. Dokumentaci může použít kdokoliv další k převzetí nebo obnovení infrastruktury.
