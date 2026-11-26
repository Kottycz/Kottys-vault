---
aliases: [Jméno domény a DNS, Jak klient najde řadič]
tags: [ops, teorie]
---

# Jméno domény a DNS

Jméno domény se volí **jednou** – při povýšení prvního řadiče – a později se mění velmi obtížně. Špatná volba se projeví až za měsíce (kolize s jinými službami, nemožnost připojit se k veřejným službám). A i s dobrým jménem je tu druhá věc, bez které doména nefunguje vůbec: **[[DNS]]**. Počítač v doméně totiž neví, který server je řadič – musí se zeptat, a ptá se právě [[DNS]].
Praxe: [[01_AD_DS]] · Předchozí: [[01b_Radice_domeny_a_FSMO]] · Navazuje: [[03b_DNS_na_radici]]

> **Jako adresa školy a telefonní seznam:** jméno domény je název školy. [[DNS]] je seznam, ve kterém si klient najde, **na jakém čísle** (adrese) sedí ředitelna (řadič). Bez seznamu zná jméno, ale nemá komu zavolat.

---

## Pojmy

- **[[DNS]] jméno domény** – jméno, podle kterého doménu hledají klienti i servery: `kotrba.cyberschool.internal`
- **[[NetBIOS]] jméno** – krátké (max 15 znaků) starší jméno domény: `KOTRBA`
- **doména nejvyšší úrovně ([[TLD]])** – poslední část jména: `cz`, `com`, `internal`
- **[[mDNS]]** – hledání zařízení v místní síti bez [[DNS]] serveru, používá doménu `.local`
- **[[SRV záznam]]** – záznam v [[DNS]], který neukazuje na počítač, ale na **službu** („řadič domény je tady“)
- **[[forwarder]]** – [[DNS]] server, kterému náš [[DNS]] předá dotaz, na který sám nezná odpověď
- **[[DNS přípona]]** – doména, která se automaticky přidá ke krátkému jménu (`srv2-fs` → `srv2-fs.kotrba.cyberschool.internal`)

## Jak pojmenovat doménu

- **nepoužívat `.local`** – koliduje s [[mDNS]] (Apple Bonjour, některé tiskárny) a dělá těžko hledatelné problémy
- **nepoužívat vymyšlené [[TLD]]** (`.lab`, `.corp`, `.skola`) – nejsou nikde rezervované, kdokoli si je může v budoucnu zaregistrovat jako veřejné a pak se jména srazí
- **v ostrém provozu** se bere **subdoména domény, kterou organizace opravdu vlastní** – škola s webem `cyberschool.cz` pojmenuje [[AD DS|AD]] třeba `ad.cyberschool.cz`
- **pro privátní a laboratorní sítě** je od 29. 7. 2024 oficiálně vyhrazená **`.internal`** (rozhodnutí [[ICANN]]) – nikdy nebude veřejná, takže nehrozí kolize
- [[NetBIOS]] jméno má max **15 znaků** a průvodce ho odvodí z prvního slova [[DNS]] jména
- bez diakritiky a mezer – jen písmena, číslice, pomlčka

### Naše konvence: `<prijmeni>.cyberschool.internal`

- `cyberschool.internal` = „jmenný prostor školy“, jako když firma vlastní `firma.cz`
- `<prijmeni>` = příjmení bez diakritiky malými písmeny (Dvořák → `dvorak`); delší než 15 znaků se zkrátí
- každý žák má **vlastní nezávislý les** a z každého výpisu (`whoami`, `gpresult`) je vidět, čí je práce

| Žák | [[DNS]] jméno | [[NetBIOS]] | Přihlášení Evy |
| :-- | :-- | :-- | :-- |
| Matěj Kotrba | `kotrba.cyberschool.internal` | `KOTRBA` | `KOTRBA\eva.student` |
| Petra Dvořáková | `dvorakova.cyberschool.internal` | `DVORAKOVA` | `DVORAKOVA\eva.student` |

## Proč AD nefunguje bez DNS

Klient neví, který server je řadič. Zjistí to **dotazem do [[DNS]] na [[SRV záznam|SRV]] záznamy**, které si řadič při povýšení sám zaregistruje:

```text
_ldap._tcp.dc._msdcs.kotrba.cyberschool.internal  →  srv1-dc.kotrba.cyberschool.internal
_kerberos._tcp.kotrba.cyberschool.internal         →  srv1-dc.kotrba.cyberschool.internal
```

Čte se to: „Kdo v doméně `kotrba.cyberschool.internal` poskytuje službu [[LDAP]] přes [[TCP]] jako řadič domény?“ Odpověď je jméno `srv1-dc`. Pak se klient zeptá [[DNS]] **podruhé** – na **[[IP adresa|IP]] adresu** toho jména (A záznam, viz [[DNS záznam]]) – a teprve teď se může k řadiči připojit. Stejně hledá i Kerberos pro ověření.

Z toho plynou dvě pravidla, která v projektu dodržujeme:

1. role **[[DNS]] Server** se instaluje spolu s [[AD DS]] na řadič (průvodce to udělá sám)
2. všechny počítače v doméně mají jako [[DNS]] server **řadič** (`192.168.16.10`), **nikdy** veřejný [[DNS]] jako `8.8.8.8` – veřejný server o naší doméně nic neví, protože existuje jen v naší síti

Jak se pak klient dostane na internet? Řadič sám předá dotazy, na které nezná odpověď (`www.skola.cz`), dál přes **forwardery** a odpověď vrátí klientovi. Klient tak potřebuje **jediný [[DNS]] server** a vyřeší si školní i internetová jména.

## Když klient doménu nenajde

Nejčastější příčina hlášky *doména nebyla nalezena* při připojování PC je **špatný [[DNS]] na klientovi**. Kontrola od nejjednoduššího:

| Krok | Příkaz na klientovi | Co hledám |
| :-- | :-- | :-- |
| 1 | `ipconfig /all` | [[DNS]] server je `192.168.16.10`, ne `8.8.8.8` ani brána |
| 2 | `ping 192.168.16.10` | řadič je dosažitelný |
| 3 | `nslookup kotrba.cyberschool.internal` | vrátí adresu řadiče |
| 4 | `nslookup -type=SRV _ldap._tcp.dc._msdcs.kotrba.cyberschool.internal` | vrátí `srv1-dc` |

- selže krok **3 nebo 4** → chyba je v [[DNS]] (špatný server na klientovi, chybějící záznamy)
- selže jen krok **2** → problém je v síti

## U nás

- doména `kotrba.cyberschool.internal`, [[NetBIOS]] `KOTRBA`
- [[DNS]] běží s [[AD DS]] na SRV1-DC a je [[DNS]] serverem celé domény
- všechny stroje mají [[DNS]] `192.168.16.10`, klientům ho předává [[DHCP]] (Modul 2)
- [[DNS]] podrobně nastavujeme v Modulu 3 ([[03a_DNS_obecne]], [[03b_DNS_na_radici]])
