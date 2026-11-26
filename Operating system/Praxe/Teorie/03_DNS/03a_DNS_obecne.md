---
aliases: [DNS obecně, Jak funguje DNS]
tags: [ops, teorie]
---

# DNS – jak se jména překládají na adresy

Ve škole bude několik serverů a desítky počítačů. Nikdo si nebude pamatovat, že souborový server je na `192.168.16.20`. A kdyby se server přestěhoval na jinou adresu, musel by to někdo oznámit všem. Proto mají počítače a služby **jména** (`srv2-fs.kotrba.cyberschool.internal`) a převod jména na [[IP adresa|IP]] zajišťuje **[[DNS]]**. Když se adresa změní, upraví se **jeden záznam** a všichni dál používají stejné jméno. Tahle poznámka vysvětluje [[DNS]] **obecně** – stejně funguje na internetu i ve škole.
Praxe: [[03_DNS]] · Další: [[03b_DNS_na_radici]] · Pojmy: [[DNS]], [[DNS záznam]]

> **Jako telefonní seznam:** jméno si zapamatuješ, číslo ([[IP adresa|IP]]) ne. [[DNS]] je obří seznam celého internetu – jen není v jedné knize, ale rozdělený mezi miliony serverů.

---

## Základní pojmy

| Pojem | Význam |
| :-- | :-- |
| **doménové jméno** | lidsky čitelné jméno, např. `www.frengp.cz`; skládá se z **návěští** (labels) oddělených tečkami |
| **[[FQDN]]** | úplné jméno až ke kořeni; formálně končí tečkou: `srv2-fs.kotrba.cyberschool.internal.` |
| **doména** | část stromu jmen, např. `cyberschool.internal` a všechno pod ní |
| **zóna** | část domény, kterou spravuje jeden autoritativní server – jedna „kniha“ záznamů |
| **záznam** | jedna položka v zóně: jméno, typ, hodnota (viz [[DNS záznam]]) |
| **resolver** | ten, kdo jméno překládá: malý v [[operační systém\|OS]] (*stub resolver*, ve Windows služba [[DNS]] Client) nebo velký u poskytovatele/ve firmě (*rekurzivní resolver*) |
| **autoritativní server** | server, který má pro zónu „oficiální“ odpověď |
| **[[DNS TTL]]** | jak dlouho (v sekundách) si smí ostatní odpověď pamatovat v cache |
| **registrátor** | firma, přes kterou si doménu koupíš; registr `.cz` spravuje sdružení **CZ.NIC** |

## Hierarchie doménových jmen

Jména tvoří **strom**, který se čte **zprava doleva**:

- **kořen** (zapisuje se `.`) – vrchol stromu; spravuje ho [[ICANN]], provozuje ho 13 „identit“ kořenových serverů (A–M); za každou stojí stovky serverů po světě se stejnou adresou (**[[anycast]]**), dotaz dorazí k nejbližšímu
- **domény nejvyšší úrovně ([[TLD]])**:
  - národní (ccTLD): `.cz`, `.sk`, `.de`
  - obecné (gTLD): `.com`, `.org`, `.net`, nové `.app`, `.cloud`
  - speciální: `.arpa` (technická infrastruktura, např. reverzní záznamy), `.internal` (privátní sítě)
- **domény druhé úrovně** – `frengp.cz`, `example.com`; ty se kupují u registrátora
- **subdomény** – všechno dál vlevo, o čem rozhoduje vlastník: `www.frengp.cz`, `srv2-fs.kotrba.cyberschool.internal`

**Delegace:** každá úroveň předává správu nižší. Kořen ví, kdo spravuje `.cz`. Servery `.cz` vědí (záznamy [[DNS záznam|NS]]), kdo spravuje `frengp.cz`. Teprve ty znají adresu `www.frengp.cz`. Nikdo nemá celý strom – a díky tomu [[DNS]] zvládne miliardy jmen.

Omezení: návěští max **63 znaků**, celé jméno max **253**, **velikost písmen nehraje roli** (`WWW.Example.COM` = `www.example.com`).

## Kdo se na překladu podílí

| Kdo | Kde běží | Co dělá |
| :-- | :-- | :-- |
| **aplikace** | prohlížeč, `ssh`, `ping` | potřebuje [[IP adresa\|IP]], zeptá se [[operační systém\|OS]] |
| **stub resolver** | v [[operační systém\|OS]] (služba [[DNS]] Client) | podívá se do souboru `hosts` a do cache, jinak se zeptá rekurzivního resolveru |
| **rekurzivní resolver** | u [[ISP]], ve firmě nebo veřejný (`1.1.1.1`, `8.8.8.8`, `9.9.9.9`) | odpověď „dohledá“ za klienta postupnými dotazy a výsledek si zapamatuje |
| **kořenové servery** | po celém světě | vědí, kdo spravuje jednotlivé [[TLD]] |
| **servery [[TLD]]** | např. `.cz` provozuje CZ.NIC | vědí, kdo spravuje domény 2. řádu |
| **autoritativní server domény** | u vlastníka nebo poskytovatele | zná skutečné záznamy, odpověď je „oficiální“ |

## Průběh dotazu

Do prohlížeče napíšeš `www.example.com` a nikdo ho nemá v cache:

1. prohlížeč se zeptá **stub resolveru** v [[operační systém|OS]]
2. stub nenajde jméno v `hosts` ani v cache → pošle dotaz **rekurzivnímu resolveru**
3. resolver se zeptá **kořenového serveru**: „Kde je `www.example.com`?“ → „Nevím, ale `.com` spravují tyto servery.“ (odkaz, *referral*)
4. zeptá se **serveru `.com`** → „Nevím, ale `example.com` spravují tyto servery.“
5. zeptá se **autoritativního serveru `example.com`** → „`www.example.com` má adresu `203.0.113.10`, platí 3600 s.“
6. resolver si odpověď uloží do **cache** a pošle ji zpět
7. stub ji předá prohlížeči (a taky si ji zapamatuje)
8. prohlížeč se připojí na [[IP adresa|IP]]

- první dotaz klienta → resolveru je **rekurzivní** (klient chce hotovou odpověď)
- kroky 3–5 jsou **iterativní** (resolver se ptá „po kouscích“ sám)
- díky cache se kroky 3–5 dělají zřídka – kořenové a [[TLD]] servery zná resolver skoro vždy z paměti

## Typy záznamů

| Typ | Co obsahuje | Příklad |
| :-- | :-- | :-- |
| **A** | IPv4 adresa | `srv2-fs.kotrba.cyberschool.internal. A 192.168.16.20` |
| **[[DNS záznam\|AAAA]]** | IPv6 adresa | `www.example.com. AAAA 2001:db8::10` |
| **[[DNS záznam\|CNAME]]** | alias – „tohle jméno je jen jiné jméno pro…“ | `ftp… CNAME srv2-fs.kotrba.cyberschool.internal.` |
| **[[DNS záznam\|MX]]** | poštovní server domény (s prioritou) | `frengp.cz. MX 10 mail.frengp.cz.` |
| **[[DNS záznam\|TXT]]** | libovolný text – ověření domény, ochrana pošty ([[SPF-DKIM-DMARC\|SPF]], [[SPF-DKIM-DMARC\|DKIM]], [[SPF-DKIM-DMARC\|DMARC]]) | `"v=spf1 include:… -all"` |
| **[[DNS záznam\|NS]]** | které servery jsou autoritativní pro zónu (delegace) | `frengp.cz. NS ns1.frengp.cz.` |
| **[[DNS záznam\|SOA]]** | „hlavička“ zóny: hlavní server, kontakt, sériové číslo, časy | jedna na zónu |
| **[[reverzní DNS\|PTR]]** | reverzní záznam: [[IP adresa\|IP]] → jméno ([[reverzní DNS]]) | `20.16.168.192.in-addr.arpa. PTR srv2-fs…` |
| **[[SRV záznam\|SRV]]** | kde běží služba (server a port); [[AD DS\|AD]] tak hledá řadič | `_ldap._tcp.dc._msdcs…` |
| **[[DNS záznam\|CAA]]** | která certifikační autorita smí vydat certifikát pro doménu | souvisí s [[HTTPS]] |

- jedno jméno může mít **víc A záznamů** → klient dostane víc adres a zkusí další, když první neodpovídá; nejjednodušší (hrubé) rozložení zátěže a ochrana proti výpadku
- **[[DNS záznam|CNAME]]** nemá vlastní adresu, vždy odkazuje na jméno s A záznamem; hodí se pro **jména služeb** – uživatelé používají `ftp…`, a když se [[FTP]] přesune, změní se jen cíl aliasu

### Reverzní záznamy

- normální dotaz: „jaká je adresa jména?“, reverzní: „jaké je jméno adresy?“
- použití: logy, poštovní servery (kontrola odesílatele), `traceroute`, ruční diagnostika
- reverzní zóny jsou ve speciální doméně `in-addr.arpa` a adresa se píše **pozpátku**: síť `192.168.16.0/24` → zóna `16.168.192.in-addr.arpa`, adresa `.20` → `20.16.168.192.in-addr.arpa`
- proč pozpátku: jména se čtou zprava (od kořene), adresy zleva (od sítě) → obrácením se adresy ve stromu seřadí od obecné části ke konkrétní a správu jde delegovat stejně jako u jmen

## Cache a TTL

Kdyby se každý dotaz ptal až autoritativního serveru, [[DNS]] by bylo pomalé a servery přetížené. Proto si odpovědi pamatují (cachují) všichni po cestě – prohlížeč, [[operační systém|OS]] i resolver. Jak dlouho, určuje **[[DNS TTL|TTL]]** v každém záznamu:

- **vysoké [[DNS TTL|TTL]]** (hodiny až den) – méně dotazů, rychlejší odpovědi, ale změna adresy se šíří pomalu
- **nízké [[DNS TTL|TTL]]** (sekundy až minuty) – změny se projeví rychle, ale dotazů je víc
- cachují se i **záporné odpovědi** („jméno neexistuje“) – když jméno založíš až po tom, co se na něj někdo ptal, chvíli ho „neuvidí“
- odtud věta „změna [[DNS]] se může projevit až za několik hodin“; zkušený správce proto **před plánovanou změnou adresy [[DNS TTL|TTL]] dočasně sníží**
- smazání cache: klient `ipconfig /flushdns`, [[DNS]] server ve Windows `Clear-DnsServerCache`

## Protokol a bezpečnost

- [[DNS]] používá port **53**: běžné dotazy přes **[[UDP]]** (rychlé, bez navazování spojení), velké odpovědi a přenosy celých zón přes **[[TCP]]**
- klasické [[DNS]] **není šifrované ani podepsané** → kdo vidí provoz, vidí, na co se ptáš, a útočník může podvrhnout odpověď (**[[DNS]] spoofing**, otrávení cache) a poslat tě na falešný server
- **[[DNSSEC]]** – autoritativní servery odpovědi **digitálně podepisují** a resolver podpis ověří; chrání proti podvržení, **ne proti odposlechu**; u `.cz` velmi rozšířené
- **[[DoH]]** ([[DNS]] over [[HTTPS]], port 443) a **[[DoH|DoT]]** ([[DNS]] over TLS, port 853) – **šifrují** dotazy mezi klientem a resolverem; [[DoH]] používají moderní prohlížeče

## Veřejná a interní jména

Ne každé jméno má být vidět z internetu – firmy a školy mají **interní jména** jen pro svou síť. Jaké zvolit?

| Volba | Problém |
| :-- | :-- |
| vymyšlená doména (`.lan`, `.corp`, `.home`) | nikdo je nerezervoval, mohou jednou vzniknout na internetu |
| `.local` | vyhrazená pro **[[mDNS]]** (automatické hledání zařízení), s klasickým [[DNS]] koliduje |
| subdoména vlastní domény (`int.frengp.cz`) | nejčistší pro firmy, ale doménu musíš vlastnit |
| **`.internal`** | **rezervovaná pro privátní použití** ([[ICANN]], červenec 2024), na internetu nikdy nebude |
| `home.arpa` | rezervovaná pro domácí sítě ([[RFC]] 8375) |

- my: `<počítač>.<prijmeni>.cyberschool.internal` – nesrazí se s žádnou skutečnou doménou a každý žák má vlastní podstrom
- **split [[DNS]]** – uvnitř sítě se jména překládají jinak (nebo jen tam) než zvenku; interní [[DNS]] odpovídá na interní jména a ostatní dotazy předává do internetu – přesně tak to funguje u nás

## DNS servery

| Server | Typ | Pozn. |
| :-- | :-- | :-- |
| **Windows Server [[DNS]]** | autoritativní i rekurzivní | integrovaný s [[AD DS\|AD]] → **náš výběr** |
| **BIND 9** | obojí | nejstarší a nejrozšířenější, „referenční“, složitější konfigurace |
| **Knot [[DNS]] / Knot Resolver** | autoritativní / rekurzivní | vyvíjí CZ.NIC, Knot [[DNS]] obsluhuje i `.cz` |
| **Unbound** | rekurzivní | rychlý a bezpečný, ověřuje [[DNSSEC]], v routerech a firewallech |
| **PowerDNS** | obojí | záznamy v databázi, má [[API]], používají ho hostingy |
| **dnsmasq** | lehký forwarder + [[DHCP]] | malý, domácí routery a laboratoře |
| **veřejné resolvery** | rekurzivní služba | `1.1.1.1` Cloudflare, `8.8.8.8` Google, `9.9.9.9` Quad9 (blokuje škodlivé domény) |

Místo [[DNS]] by šel **soubor `hosts`** na každém počítači – ale platí jen pro jeden počítač a každou změnu musíš udělat ručně všude → neškáluje.

## Diagnostika – když „to nejde“

| Nástroj | Použití |
| :-- | :-- |
| [[nslookup]] `<jméno>` | základní dotaz; `nslookup <jméno> <server>` zeptá se konkrétního serveru; `-type=SRV` jiný typ záznamu |
| `Resolve-DnsName <jméno>` | PowerShell – podrobná odpověď včetně typu a [[DNS TTL\|TTL]]; `-Server`, `-Type` |
| `ipconfig /all` | které [[DNS]] servery klient používá |
| `ipconfig /displaydns` | co má klient v cache |
| `ipconfig /flushdns` | smaže cache klienta |
| `ping <jméno>` | rychlé ověření, že se jméno přeloží (ping může blokovat firewall) |

Typické odpovědi ([[NXDOMAIN]]):

- **Non-existent domain / [[NXDOMAIN]]** – jméno neexistuje (překlep, záznam chybí, ptáš se špatného serveru)
- **[[NXDOMAIN|SERVFAIL]]** – server odpověď nezjistil (chyba konfigurace, nedostupný nadřazený server, chyba [[DNSSEC]])
- **[[DNS]] request timed out** – server neodpovídá (neběží, blokovaný port 53, špatná [[IP adresa|IP]] serveru)

Postup, když se server podle jména nenačte:

1. funguje to přes **[[IP adresa|IP]]**? Pokud ne, problém není v [[DNS]] (síť, služba, firewall)
2. `ipconfig /all` – používá klient správný [[DNS]] server?
3. `nslookup <jméno> <IP DNS serveru>` – odpovídá server správně, když se ho zeptáš přímo?
4. server odpovídá správně, ale počítač ne → chyba v nastavení klienta nebo stará cache (`ipconfig /flushdns`)

## U nás

- [[DNS]] běží na **SRV1-DC** spolu s [[AD DS|AD]] a spravuje zónu `kotrba.cyberschool.internal`
- klienti i servery mají [[DNS]] `192.168.16.10`, klientům ho dává [[DHCP]] (option 006)
- ostatní dotazy (internet) SRV1-DC předá dál (forwarder) → počítači stačí jediný [[DNS]]
- v zóně: **A** pro servery a klienty, **[[DNS záznam|CNAME]]** `ftp` jako jméno služby, **[[reverzní DNS|PTR]]** v reverzní zóně
- jak to funguje přímo na řadiči: [[03b_DNS_na_radici]]
