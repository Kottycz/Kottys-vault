---
aliases: [Doména a Active Directory, Teorie AD DS]
tags: [ops, teorie]
---

# Doména a Active Directory

Dnes se ve škole přihlašuje lokálními účty, které existují na každém počítači zvlášť, často se stejným heslem. Změníš heslo na jednom PC, na ostatních zůstane staré. Žák odejde a jeho účet se musí mazat ručně všude. A nikdo neví, kdo má k čemu přístup. Řešením je **jedna centrální evidence** lidí, počítačů a skupin, kterou spravuje server – ve Windows je to **Active Directory Domain Services**.
Praxe: [[01_AD_DS]] · Další: [[01b_Radice_domeny_a_FSMO]] · [[01c_Jmeno_domeny_a_DNS]]

> **Jako školní matrika s vrátnicí:** matrika ví, kdo ke škole patří a do jaké třídy chodí (evidence). Vrátnice ověří, jestli je člověk ten, za koho se vydává, a podle seznamu rozhodne, kam smí. Doména dělá obojí pro celou školu.

---

## Pracovní skupina × doména

Každý nově nainstalovaný Windows je v **pracovní skupině**: má vlastní lokální databázi účtů (**[[SAM]]**) a o ostatních počítačích nic neví. Tak dosud fungovala škola – Eva má na každém PC účet `student` se stejným heslem.

**Doména** to obrací: existuje **jedna databáze** uživatelů, počítačů a skupin na serveru (řadiči domény). Počítač se do domény **připojí (join)** a od té chvíle neověřuje uživatele sám, ale ptá se řadiče. Eva má jeden účet `eva.student`, který funguje na kterémkoli školním PC, a heslo mění jednou.

| | Pracovní skupina | Doména |
| :-- | :-- | :-- |
| kde jsou účty | na každém PC zvlášť | na řadiči, jedna kopie pro všechny |
| změna hesla | na každém PC znovu | jednou, platí všude |
| oprávnění | nastavují se na každém PC | podle skupin, centrálně |
| pravidla pro PC | ručně na každém stroji | centrálně přes [[GPO]] (Modul 5) |
| vhodné pro | doma, pár PC | škola, firma, desítky PC |

## Co je AD DS

**[[AD DS]]** je role Windows Serveru, která z obyčejného serveru udělá **[[řadič domény]]**. Je to **adresářová služba** se čtyřmi úkoly:

| Úkol | Otázka | Příklad |
| :-- | :-- | :-- |
| **evidence (adresář)** | kdo existuje, v jaké skupině, kde v organizaci | Eva je žákyně informatiky, je ve skupině `GG_Studenti_IT` |
| **autentizace (ověření)** | jsi opravdu ten, za koho se vydáváš? | Eva zadá na PC1-WIN jméno a heslo, SRV1-DC ho ověří |
| **autorizace** | co smíš? | Eva smí číst složku `Verejne`, ale ne `Vedeni` |
| **centrální správa** | nastavení jednou, platí všude | [[GPO]] zakáže žákům Ovládací panely |

### Pojmy, které se budou vracet

- **[[NTDS.dit]]** – soubor s databází [[AD DS|AD]] na každém řadiči (`C:\Windows\NTDS`)
- **[[SYSVOL]]** – sdílená složka na řadiči se zásadami skupiny ([[GPO]]) a přihlašovacími skripty; klienti si z ní při přihlášení stahují pravidla
- **[[LDAP]]** (port 389) – protokol, kterým se nástroje a aplikace ptají adresáře („najdi uživatele `eva.student`“)
- **[[Kerberos]]** (port 88) – protokol pro ověření; po přihlášení dostaneš od řadiče „vstupenku“ (*ticket*) a tou se prokazuješ dalším serverům, heslo už se po síti znovu neposílá; je citlivý na čas
- **[[DNS]]** – bez něj klienti řadič vůbec nenajdou (viz [[01c_Jmeno_domeny_a_DNS]])

## Logická struktura: les → strom → doména → OU → objekt

[[AD DS|AD]] je hierarchie „krabic v krabicích“:

| Pojem | Co to je | U nás |
| :-- | :-- | :-- |
| **les (forest)** | nejvyšší úroveň a **hranice zabezpečení**; všechny domény v lese sdílí **schéma** (jaké typy objektů a atributů existují) a konfiguraci | jeden les, vznikne s první doménou; **každý žák má vlastní les** |
| **strom (tree)** | domény se souvislým jménem (`cyberschool.internal` a pod ní `brno.cyberschool.internal`) | jeden strom s jednou doménou |
| **doména** | základní jednotka správy; má [[DNS]] jméno a kratší [[NetBIOS]] jméno | `kotrba.cyberschool.internal`, [[NetBIOS]] `KOTRBA` |
| **[[OU]]** | „složka“ uvnitř domény na třídění objektů; **lze na ni navázat [[GPO]]** a delegovat správu | `Skola`, `Skola\Studenti\Informatika`… (Modul 4) |
| **kontejner** | taky složka, ale **[[GPO]] na něj nejde**; vzniká automaticky | `Users`, `Computers`, `Builtin` → proto zakládáme vlastní [[OU]] `Skola` |
| **objekt** | konkrétní položka s atributy (jméno, heslo, členství) | uživatel, počítač, skupina |
| **lokalita (site)** | fyzické umístění – podsítě spojené rychlou linkou; řídí, který řadič klient použije a jak často se replikuje | `Default-First-Site-Name` |

> **Záludnost:** `Domain Controllers` vypadá v [[ADUC]] jako kontejner, ale je to **[[OU]]** (proto je na ní výchozí *Default Domain Controllers Policy*). `Users` a `Computers` jsou opravdu kontejnery.

### Typy objektů

| Objekt | K čemu | Příklad | Kde leží |
| :-- | :-- | :-- | :-- |
| uživatel | účet člověka | `eva.student`, `jana.teacher` | `Skola\Studenti\…`, `Skola\Zamestnanci\…` |
| počítač | účet počítače – i počítač se v doméně „přihlašuje“ | `PC1-WIN`, `SRV2-FS` | `Skola\Pocitace\…`, `Domain Controllers` |
| globální skupina (`GG_`) | lidé **podle role** | `GG_Studenti_IT`, `GG_Ucitele` | `Skola\Skupiny` |
| doménová lokální skupina (`DL_`) | **oprávnění ke zdroji** | `DL_FS_Verejne_Cteni` (Modul 7) | `Skola\Skupiny` |
| servisní účet | účet pro službu, ne pro člověka | zatím žádný | `Skola\Sluzebni-ucty` |
| [[GPO]] | sada pravidel, linkuje se na [[OU]] | `Studenti-Omezeni` (Modul 5) | v `SYSVOL` |
| sdílená tiskárna | publikovaná v [[AD DS\|AD]], aby ji lidé našli | Modul 8 | pod počítačem `SRV2-FS` |

### Jak se objekt jmenuje

Jeden uživatel má v [[AD DS|AD]] několik identifikátorů a různé nástroje ukazují různé:

| Identifikátor | Hodnota (Eva) | Kde ho uvidíš |
| :-- | :-- | :-- |
| **[[DN]]** – úplná cesta v adresáři | `CN=Eva Svobodová,OU=Informatika,OU=Studenti,OU=Skola,DC=kotrba,DC=cyberschool,DC=internal` | PowerShell (`-Path`, `-SearchBase`), ADSI Edit |
| **[[UPN]]** – jméno jako e-mail | `eva.student@kotrba.cyberschool.internal` | přihlašovací obrazovka |
| **sAMAccountName** s doménou | `KOTRBA\eva.student` | `whoami`, oprávnění NTFS, [[FTP]] |
| **[[SID]]** | `S-1-5-21-…-1104` | oprávnění na souborech |

- [[DN]] se čte **zprava doleva** jako adresa na obálce: doména → [[OU]] `Skola` → `Studenti` → `Informatika` → Eva
- **proč [[SID]] a ne jméno:** jméno se může změnit (svatba, překlep), ale oprávnění se nemají ztratit → oprávnění ukazují na [[SID]], který se nemění
- když účet **smažeš a založíš znovu** se stejným jménem, dostane **nový [[SID]]** → ke starým souborům přístup nemá

## Na AD stojí další moduly

- **Modul 2–3** – [[DHCP]] a [[DNS]] obsluhují počítače v doméně
- **Modul 4** – [[OU]] podle oborů a rolí, skupiny, účty všech postav
- **Modul 5** – zásady skupiny navázané na [[OU]]
- **Modul 6–7** – oprávnění ke složkám a [[FTP]] pro doménové skupiny
- **Modul 8** – tiskárny podle [[OU]] a skupin

## U nás

- **jedna doména s jedním řadičem** (SRV1-DC) – jednoduché na stavbu i pochopení; nevýhoda: když řadič vypadne, nikdo se nepřihlásí
- **vlastní strom [[OU]] `Skola`** místo výchozích kontejnerů (na ty nejde [[GPO]])
- **každý žák má vlastní les** – nezávislé prostředí, zásahy jednoho neovlivní ostatní a z každého výpisu je vidět, čí je práce
