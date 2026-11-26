---
aliases: [Řadiče domény a role, FSMO teorie]
tags: [ops, teorie]
---

# Řadiče domény – replikace a role

Řadič domény je **nejdůležitější server školy**. Když přestane fungovat, nepřihlásí se nikdo – žáci ani učitelé – a přestane i [[DNS]], takže se počítače nenajdou ani mezi sebou. Proto je dobré vědět, co přesně řadič drží, jak se jeho data dostanou na další řadič a které úkoly smí dělat vždycky jen jeden z nich.
Praxe: [[01_AD_DS]] · Předchozí: [[01a_Domena_a_AD]] · Další: [[01c_Jmeno_domeny_a_DNS]]

> **Jako ředitelna se dvěma kopiemi matriky:** změna v jedné kopii (nový žák) se opíše do druhé. Když jedna shoří, škola pořád ví, kdo k ní patří. Ale pečeť a rozvrh má na starosti vždy jen jeden člověk, jinak by byl chaos.

---

## Fyzická struktura – kde data leží

Logická struktura (les, doména, [[OU]]) popisuje, *jak jsou data uspořádaná*. Fyzická popisuje, *kde skutečně leží* – na řadičích domény:

- každý [[řadič domény]] má **plnou kopii** databáze své domény ([[NTDS.dit]])
- řadiče jsou si **rovnocenné**: změnu (nový uživatel, nové heslo) jde udělat na kterémkoli a ostatní si ji převezmou = **multi-master replikace**
- uvnitř jedné lokality (site) se replikuje rychle, mezi lokalitami podle plánu, aby se šetřila pomalá linka
- v reálném provozu mají organizace **vždy aspoň dva řadiče** – když jediný vypadne, nefunguje přihlašování ani [[DNS]]
- my máme kvůli jednoduchosti jen SRV1-DC; adresa `.30` je rezervovaná pro druhý řadič SRV3-DC, který jen popisujeme teoreticky

### Záloha řadiče

- řadič **nejde zálohovat jako obyčejný soubor ani vracet snapshotem**
- kdyby existovaly dva řadiče a jeden se vrátil do staršího stavu, posílal by data, která ostatní už přepsali → replikace se dostane do rozporu = **[[USN rollback]]**
- nové Windows Servery mají ochranu *VM-GenerationID*, ale správná záloha je přes **stav systému (System State)**
- snapshot je u nás pomůcka pro výuku, ne záloha (viz [[snapshot]])

## Role serverů v doméně

| Role | Co dělá | U nás |
| :-- | :-- | :-- |
| **řadič domény ([[řadič domény\|DC]])** | drží kopii [[AD DS\|AD]], ověřuje uživatele | **SRV1-DC** `.10` |
| **další řadič (Additional [[řadič domény\|DC]])** | stejná data a práva jako první; odolnost a rozložení zátěže; v průvodci *Add a domain controller to an existing domain* | SRV3-DC `.30` – jen teorie |
| **[[RODC]]** | řadič jen pro čtení s neúplnou kopií hesel; pro pobočky, kde server není fyzicky zabezpečený | nepoužíváme |
| **členský server (Member Server)** | je v doméně, poskytuje služby (soubory, tisk, web), ale uživatele **neověřuje** a databázi [[AD DS\|AD]] nemá | **SRV2-FS** `.20` |
| **samostatný server (Standalone)** | server mimo doménu, v pracovní skupině | SRV2-FS před připojením (Modul 0) |
| **klient** | pracovní stanice v doméně | **PC1-WIN** `.100–.200` |

## FSMO – operace, které smí dělat jen jeden

I když jsou řadiče rovnocenné, existuje pět operací, u kterých by souběžné změny na víc řadičích způsobily konflikt. Proto je dělá vždy **jen jeden určený řadič**. Říká se jim role **[[FSMO]]** (*Flexible Single Master Operations*, čti „fizmo“).

| Role | Platí pro | Co dělá | Když řadič s rolí vypadne |
| :-- | :-- | :-- | :-- |
| **Schema Master** | celý les | jediný smí měnit schéma [[AD DS\|AD]] (např. při instalaci Exchange) | nejde rozšířit schéma, běžně nepoznáš |
| **Domain Naming Master** | celý les | jediný smí přidat/odebrat doménu v lese | nejde přidat doménu, běžně nepoznáš |
| **[[FSMO\|RID]] Master** | doména | přiděluje řadičům bloky čísel ([[FSMO\|RID]]), ze kterých vznikají [[SID]] nových objektů | po vyčerpání bloku nejde zakládat uživatele a skupiny |
| **[[FSMO\|PDC]] Emulator** | doména | hlavní zdroj **času**, hned se dozví o změně hesla, řeší zamykání účtů, výchozí cíl pro úpravy [[GPO]] | **poznáš nejdřív** – rozjedou se hodiny (Kerberos přestane fungovat), problémy se změnou hesla |
| **Infrastructure Master** | doména | udržuje odkazy na objekty z jiných domén | v lese s jednou doménou bez dopadu |

- první řadič nového lesa dostane **všech pět rolí** automaticky → u nás SRV1-DC
- ověření: `netdom query fsmo`, nebo PowerShell:
  ```powershell
  Get-ADForest | Select-Object SchemaMaster, DomainNamingMaster
  Get-ADDomain | Select-Object PDCEmulator, RIDMaster, InfrastructureMaster
  ```
- **transfer** = řádné předání role jinému řadiči (plánovaná výměna)
- **seize** = násilné převzetí, když je původní řadič trvale mrtvý; je to krajní řešení – starý řadič se pak **nikdy nesmí vrátit** do sítě v původním stavu

## Global Catalog

- **[[Global Catalog]] ([[Global Catalog|GC]])** = zkrácený výpis (jen hlavní atributy) **všech objektů celého lesa** pro rychlé hledání napříč doménami
- při přihlášení se z něj zjišťuje členství v univerzálních skupinách
- v lese s jednou doménou ho má typicky každý řadič, tedy i SRV1-DC – v průvodci povýšení zůstává zaškrtnuté *Global Catalog ([[Global Catalog|GC]])*

> **Primární × sekundární?** Tahle slova se dnes používají u **[[DNS]] zón** (primární zóna je zapisovatelná, sekundární jen kopie pro čtení – Modul 3), ne u řadičů domény.

## Funkční úroveň lesa a domény

- určuje, **jaké funkce [[AD DS|AD]]** smí les/doména používat, a zároveň **nejstarší verzi Windows Serveru**, která smí být řadičem
- Windows Server 2025 přinesl úroveň **2025** (v bezobslužné instalaci `ForestLevel 10` / `DomainLevel 10`), potřebnou mj. pro novou 32k velikost stránky databáze
- nový les na Serveru 2025 musí mít úroveň aspoň **2016**
- úroveň jde jen **zvýšit, ne snížit**; protože všechny naše řadiče jsou 2025, necháváme v průvodci nabídnutou hodnotu

## U nás

- jeden řadič **SRV1-DC** – drží všech 5 [[FSMO]], je Global Catalog a provozuje [[DNS]]
- **SRV2-FS** bude členský server – soubory, [[FTP]], tisk; uživatele neověřuje
- **PC1-WIN** je klient
- služby **ne přímo na řadiči** – řadič je kritický, nemá se přetěžovat ani ohrožovat
