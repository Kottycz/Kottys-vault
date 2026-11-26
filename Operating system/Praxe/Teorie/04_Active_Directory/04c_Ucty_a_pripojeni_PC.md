---
aliases: [Uživatelské účty a připojení PC, Join do domény]
tags: [ops, teorie]
---

# Uživatelské účty a připojení počítače do domény

Struktura [[OU]] a skupiny jsou zatím jen prázdné obaly. Aby se ve škole dalo pracovat, potřebujeme **uživatelské účty** pro lidi a **počítačové účty** pro stroje. Pak se každý žák a učitel přihlásí svým jménem na kterémkoli počítači v doméně a dostane své prostředí.
Předchozí: [[04b_Skupiny_a_AGDLP]] · Základy: [[01a_Domena_a_AD]]

> **Jako průkaz a zámek:** uživatelský účet je průkaz, který ukazuje člověk. Počítačový účet je „průkaz“ samotného počítače – i počítač se řadiči musí prokázat, než mu bude důvěřovat.

---

## Pojmy

| Pojem | Význam |
| :-- | :-- |
| **uživatelský účet** | objekt v [[AD DS\|AD]], který reprezentuje osobu a umožní jí přihlášení |
| **počítačový účet** | objekt v [[AD DS\|AD]], který reprezentuje počítač nebo server po připojení do domény |
| **přihlašovací jméno** (`sAMAccountName`) | krátké jméno, např. `eva.student` |
| **[[UPN]]** | přihlašovací jméno ve tvaru e-mailu: `eva.student@kotrba.cyberschool.internal` |
| **[[NetBIOS]] jméno domény** | `KOTRBA` → přihlášení `KOTRBA\eva.student` |
| **zásady hesel** | pravidla pro heslo (délka, složitost, stáří); nastavuje je [[GPO]] |
| **domovská složka** | síťová složka uživatele připojená jako disk (`H:`) |
| **šablona uživatele** | vzorový účet, jehož kopírováním se zakládají další |
| **[[secure channel]]** | důvěryhodný vztah počítače k řadiči, založený na tajném hesle počítačového účtu |

## Uživatelský účet

| Atribut | Příklad | Pozn. |
| :-- | :-- | :-- |
| celé jméno (*Full name*) | `Eva Svobodová` | s diakritikou, zobrazuje se |
| přihlašovací jméno (*User logon name*) | `eva.student` | **bez diakritiky**, v doméně se nesmí opakovat |
| [[UPN]] přípona | `@kotrba.cyberschool.internal` | nabídne se sama |
| jméno pro starší systémy | `KOTRBA\eva.student` | [[NetBIOS]] jméno domény + přihlašovací jméno |
| [[OU]] | `Skola\Studenti\Informatika` | podle role a oboru |
| skupiny | `GG_Studenti_IT` | oprávnění |
| domovská složka | `H:` → `\\SRV1-DC\home$\eva.student` | viz níže |
| stav | zapnutý (*Enabled*) | zakázaný účet se nepřihlásí, ale zůstává v [[AD DS\|AD]] |

- přihlásit se jde třemi rovnocennými způsoby: `eva.student@kotrba.cyberschool.internal` ([[UPN]]), `KOTRBA\eva.student`, nebo jen `eva.student` (v rámci domény)
- pro oprávnění systém nepoužívá jméno, ale **[[SID]]** → smazaný a znovu založený účet stejného jména je pro systém **jiný uživatel**

## Hesla a zásady hesel

Pravidla pro hesla se nastavují **zásadami skupiny** ([[GPO]], Modul 5), ne přímo v [[ADUC]]. Výchozí *Default Domain Policy* obvykle nastavuje:

| Nastavení | Obvyklá výchozí hodnota |
| :-- | :-- |
| minimální délka | 7 znaků |
| složitost | zapnuto – 3 ze 4 druhů znaků (malá, velká, číslice, symboly), nesmí obsahovat jméno účtu |
| maximální stáří | 42 dní |
| historie hesel | 24 zapamatovaných |
| zamknutí po chybných pokusech | vypnuto |

- přesné hodnoty: Default Domain Policy → Computer Configuration → Policies → Windows Settings → Security Settings → **Account Policies**
- dnešní doporučení se od klasických pravidel (časté změny, hodně symbolů) liší: **delší heslo nebo věta**, žádné opakování hesel z jiných služeb, kontrola proti uniklým heslům a **vícefázové ověření ([[MFA]])**
- v projektu jednoduché učební heslo (viz [[Rules]]) – splňuje výchozí složitost a zná ho celá třída → **v ostrém provozu nepoužitelné**
- **User must change password at next logon** donutí uživatele po prvním přihlášení heslo změnit – v praxi správně, v projektu ho odškrtáváme, aby se přihlašování nekomplikovalo

## Zakládání účtů

| Způsob | Kdy se hodí | Pozn. |
| :-- | :-- | :-- |
| **ručně v [[ADUC]]** (New → User) | pár účtů | pomalé a náchylné na překlepy |
| **kopie šablony** (Copy) | desítky účtů se stejným nastavením | vzorový účet nese společné věci (skupiny, domovskou složku) |
| **PowerShell** (`New-ADUser`, často import z CSV) | stovky účtů, opakované zakládání | rychlé a opakovatelné, ve smyčce |

Dává smysl začít jedním účtem ručně, pochopit jeho atributy, a pak přejít na skript. Při hromadném zakládání žáků (každý rok nový ročník) je skript jediná rozumná cesta.

## Domovské složky

- **domovská složka** (*home folder*) je síťová složka uživatele, která se po přihlášení připojí jako disk (`H:`)
- soubory jsou **na serveru, ne na konkrétním PC** → uživatel k nim má přístup z jakéhokoli počítače v doméně a server je zálohuje
- nastavení v [[ADUC]]: záložka **Profile → Home folder → Connect** → disk `H:` a cesta `\\SRV1-DC\home$\%username%`
  - `%username%` se nahradí přihlašovacím jménem
  - `$` na konci jména sdílení = **skryté sdílení**
- oprávnění se nastaví tak, aby každý viděl **jen svou** složku
- v Modulu 4 je domovská složka na SRV1-DC **jen provizorně**, v Modulu 6–7 ji převezme SRV2-FS

## Kočovné profily

**Profil** uživatele je jeho osobní prostředí – plocha, dokumenty, nastavení aplikací a registrový soubor `NTUSER.DAT`. Normálně je **lokální**: vznikne při prvním přihlášení na daném PC a zůstane tam. Na jiném PC uživatel začíná s prázdným profilem.

**[[kočovný profil]]** (*roaming profile*) to řeší:

- po odhlášení se profil **zkopíruje na server**, při dalším přihlášení (kdekoli v doméně) se **stáhne zpět**
- nastavení v [[ADUC]]: záložka **Profile → Profile path** = `\\SRV1-DC\profiles$\%username%`
- složku uživatele nezakládáš ručně – vytvoří ji Windows při prvním odhlášení a přidá příponu verze profilu (`eva.student.V6`)
- oprávnění na kořeni `C:\profiles` jsou jiná než u domovských složek: uživatel smí v kořeni jen **vytvořit** svou složku a vypsat obsah; plná práva má jen na svou podsložku (přes `CREATOR OWNER`) a `Administrators`

**Domovská složka × profil:** domovská složka (`H:`) je místo, kam uživatel **záměrně** ukládá soubory. Profil je **prostředí**, které Windows ukládá samo. Obojí patří na server, a to na odolné úložiště – proto se v Modulu 7 přesunou na SRV2-FS.

Kočovné profily nejsou jediná možnost – moderní alternativy jsou FSLogix (profil jako VHDx, typicky ve VDI) nebo Enterprise State Roaming v cloudu. Pro učebnu v doméně a pochopení principu jsou kočovné profily nejpřímější.

## Počítačový účet a připojení do domény

Počítač se do domény **připojí** a v [[AD DS|AD]] pro něj vznikne **počítačový účet**:

1. **počítač najde řadič** – zeptá se [[DNS]] na [[SRV záznam|SRV]] záznamy domény; proto musí mít jako [[DNS]] server **řadič** (viz [[03b_DNS_na_radici]]); se špatným [[DNS]] se objeví *doména nebyla nalezena*
2. **ověření** – zadáš účet, který smí přidávat počítače do domény (u nás `Administrator`)
3. **vznikne počítačový účet** ve výchozím kontejneru `Computers`; počítač a řadič si dohodnou **tajné heslo** počítačového účtu → vznikne **secure channel**
4. **restart** – po něm se počítač hlásí jako člen domény a nabídne přihlášení doménovým účtem
5. **přesun do [[OU]]** – objekt přesuneme z `Computers` do `Pocitace\Klienti-Ucebny`, aby na něj platily [[GPO]] (na kontejner [[GPO]] nejde)

Co musí platit **předem**:

- **[[DNS]]** – klient používá řadič jako [[DNS]] server
- **čas** – rozdíl mezi klientem a řadičem nejvýš **5 minut**, jinak selže [[Kerberos]]
- **síť** – klient řadič dosáhne (ping, firewall neblokuje)

- nový počítačový objekt vzniká vždy v `Computers`; jde to změnit příkazem `redircmp`, ale pro naši školu je jednodušší objekt po připojení přesunout ručně nebo skriptem

### Doménový × lokální účet

- **doménový účet** (`KOTRBA\eva.student`) – heslo ověří řadič; přihlásíš se kdekoli v doméně a máš stejné prostředí
- **lokální účet** (`.\Administrator`) – existuje jen na tom jednom PC; slouží jen k nouzové správě

### Když se uživatel nepřihlásí

Ověř postupně: je účet **zapnutý**, správné **heslo**, má klient správný **[[DNS]]**, sedí **čas** s řadičem, je PC opravdu **v doméně**.

## U nás

- 10 uživatelských účtů (2 učitelé, ředitel, hospodářka, 6 žáků) ve správných [[OU]] a skupinách
- všem učební heslo a odškrtnutá změna hesla při prvním přihlášení
- provizorní domovské složky `C:\home` a kočovné profily `C:\profiles` na SRV1-DC, nastavené všem uživatelům
- **PC1-WIN** připojený do domény a přesunutý do `Pocitace\Klienti-Ucebny`
- ověření, že se každá postava přihlásí na stejném PC svým účtem
