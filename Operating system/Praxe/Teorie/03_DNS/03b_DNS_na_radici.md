---
aliases: [DNS na řadiči domény, DNS ve Windows a AD]
tags: [ops, teorie]
---

# DNS na řadiči domény

Role **[[DNS]] Server** se na SRV1-DC nainstalovala už v Modulu 1 spolu s [[AD DS|AD]] a řadič si do [[DNS]] sám zapsal záznamy, podle kterých ho klienti hledají. Jakmile ale přibude druhý server a klienti, je potřeba vědět, **co si [[DNS]] zapíše samo a co musí správce doplnit ručně**. Hlavně **reverzní zóna** (adresa → jméno) nevzniká automaticky – bez ní nefunguje zpětné vyhledávání a některé nástroje se chovají divně. Obecné principy [[DNS]] jsou v [[03a_DNS_obecne]].
Praxe: [[03_DNS]] · Předchozí: [[03a_DNS_obecne]] · Pojmy: [[DNS záznam]], [[reverzní DNS]]

> **Jako školní seznam kontaktů:** nový učitel se do seznamu zapíše sám (dynamická aktualizace). Ale „obrácený seznam“ (podle čísla najít jméno) musí někdo nejdřív založit, a teprve pak se do něj záznamy dostanou.

---

## Pojmy

| Pojem | Význam |
| :-- | :-- |
| **dopředná zóna** (Forward Lookup Zone) | jméno → adresa; u nás `kotrba.cyberschool.internal` |
| **reverzní zóna** (Reverse Lookup Zone) | adresa → jméno ([[reverzní DNS\|PTR]]); u nás `16.168.192.in-addr.arpa` |
| **zóna integrovaná s [[AD DS\|AD]]** | uložená v databázi [[AD DS\|AD]] místo v souboru, replikuje se mezi řadiči |
| **dynamic update** | klienti, servery a [[DHCP]] si zapisují záznamy do [[DNS]] sami |
| **secure dynamic update** | zapisovat smí jen ověření členové domény; jen v zónách integrovaných s [[AD DS\|AD]] |
| **[[SRV záznam]] řadiče** | podle něj klienti najdou řadič (`_ldap._tcp.dc._msdcs…`) |
| **[[forwarder]]** | server, kterému se předají dotazy, na které naše [[DNS]] neumí odpovědět |
| **conditional forwarder** | forwarder jen pro vybranou doménu |
| **[[forwarder\|root hints]]** (kořenové nápovědy) | seznam kořenových serverů, od kterých server začne hledat, když nemá forwarder |
| **[[scavenging]]** | automatické mazání zastaralých dynamických záznamů; výchozí vypnuté |
| **[[DNS]] Manager** | konzole pro správu [[DNS]] (Server Manager → Tools → [[DNS]], `dnsmgmt.msc`) |

## Typy zón

| Typ | Co to je |
| :-- | :-- |
| **Primary** | autoritativní zdroj zóny – tady se záznamy vytvářejí a mění; v souboru nebo v [[AD DS\|AD]] |
| **Secondary** | kopie primární zóny jen pro čtení, získaná **přenosem zóny** ([[zone transfer]]); nejde integrovat s [[AD DS\|AD]] |
| **Stub** | obsahuje jen [[DNS záznam\|NS]] záznamy – kdo je pro zónu autoritativní; propojuje jmenné prostory |

**Klasická primární zóna** má jen jednu zapisovatelnou kopii – když ten server vypadne, záznamy nejdou měnit, sekundární jen čtou.

**Zóna integrovaná s [[AD DS|AD]]** je uložená v databázi Active Directory:

- každý řadič s [[DNS]] má **plnou zapisovatelnou kopii** a změny se replikují spolu s [[AD DS|AD]]
- žádné samostatné soubory ani ruční přenosy zón
- záznamy jde měnit na kterémkoli řadiči → výpadek jednoho nevadí
- umí **bezpečné dynamické aktualizace**
- přístup se řídí oprávněními ([[ACL]]) v [[AD DS|AD]]
- při vytváření se volí **rozsah replikace**: řadiče v doméně / v celém lese / vybrané; my volíme **řadiče v této doméně** (tak vznikla i zóna `kotrba.cyberschool.internal` při povýšení)

## Kdo zapisuje záznamy

| Cesta | Kdo | Co |
| :-- | :-- | :-- |
| **automaticky** při povýšení a startu řadiče | služba **[[Netlogon]]** | A záznam řadiče a [[SRV záznam\|SRV]] záznamy (složky `_msdcs`, `_sites`, `_tcp`, `_udp` v zóně) |
| **dynamicky** | klient nebo server (služba [[DHCP]] Client); [[DHCP]] server může zapsat za klienta | vlastní A, často i [[reverzní DNS\|PTR]] |
| **ručně** | správce v [[DNS]] Manageru nebo PowerShellu | stroje, které ještě neexistují (SRV2-FS), aliasy [[DNS záznam\|CNAME]] |

### Dynamické aktualizace a zabezpečení

Ve vlastnostech zóny (záložka General) se nastavuje, kdo smí zapisovat sám:

| Volba | Kdo smí | Použití |
| :-- | :-- | :-- |
| **None** | nikdo, všechno ručně | statické prostředí |
| **Nonsecure and secure** | kdokoli v síti, i bez ověření | nevhodné – útočník podvrhne záznam |
| **Secure only** | jen ověřený člen domény (ověří [[Kerberos]]) | **naše volba** |

- při bezpečné aktualizaci záznam **„vlastní“** počítač, který ho vytvořil → jiný počítač ho nepřepíše
- doporučení: klienty nechat zapisovat se sami, ručně přidávat jen to, co jinak nevznikne
- staré záznamy zaniklých počítačů se samy nemažou → **scavenging** (výchozí vypnutý); v malé síti stačí zónu občas zkontrolovat ručně

### Řadič se dvěma síťovými kartami

- SRV1-DC má školní (Ethernet1) a internetovou (Ethernet0) kartu → dynamická registrace zapíše **adresy obou** → v zóně jsou **dva** záznamy `srv1-dc`
- klient pak může dostat adresu internetové karty, na kterou se ve školní síti nedostane
- proto se v postupu bere záznam s **lokální adresou** a v [[DHCP]] (option 006) je jen `.10`, ne adresa internetové karty
- přesně tohle jsem řešil v Modulu 3: `srv1-dc` má `192.168.16.10` i `10.70.32.245`; [[DNS]] server klientovi z lokální sítě dává `.10` jako první

## Reverzní zóna a PTR

Reverzní zóna odpovídá na otázku „jaké jméno má tahle adresa?“. Adresa se píše **pozpátku** pod `in-addr.arpa` a záznam [[reverzní DNS|PTR]] se jmenuje posledním číslem adresy.

- reverzní zóna **nevznikne sama** – správce ji založí: New Zone → Reverse Lookup Zone → Network ID `192.168.16` → `16.168.192.in-addr.arpa`; volíme **integrovanou s [[AD DS|AD]]** a **Secure only**
- **A záznam, který existoval před vytvořením reverzní zóny, [[reverzní DNS|PTR]] nemá** – to se týká právě **SRV1-DC**; doplní se v [[GUI]] odškrtnutím a zaškrtnutím *Update associated pointer ([[reverzní DNS|PTR]]) record* u A záznamu, nebo `Add-DnsServerResourceRecordPtr`
- při přidávání nového A záznamu zaškrtni **Create associated pointer ([[reverzní DNS|PTR]]) record** / v PowerShellu `-CreatePtr` – funguje jen tehdy, když reverzní zóna **už existuje**
- když reverzní zóna chybí, `nslookup` hned při spuštění hlásí `Can't find server name for address 192.168.16.10: Non-existent domain` – zkouší totiž zjistit jméno vlastního [[DNS]] serveru zpětným dotazem; dotazy na jména přitom fungují dál
- [[reverzní DNS|PTR]] se hodí v logách, při diagnostice (`ping -a`, `tracert`), u služeb, které ověřují klienta, a při kontrole, že jméno sedí s adresou

## Alias CNAME pro služby

SRV2-FS bude poskytovat soubory i [[FTP]] (Modul 7). Uživatelé se ale nemají připojovat na **jméno serveru**, nýbrž na **jméno služby**:

```text
ftp.kotrba.cyberschool.internal.  CNAME  srv2-fs.kotrba.cyberschool.internal.
```

- když se [[FTP]] jednou přestěhuje na jiný server, změní se jen cíl aliasu a uživatelé nic nepoznají
- alias musí ukazovat na jméno, které má A záznam → zakládá se až **po** A záznamu SRV2-FS
- druhý A záznam místo aliasu by fungoval taky, ale při změně adresy by se upravovaly dva záznamy
- `nslookup ftp.kotrba.cyberschool.internal` ukáže jméno cíle (*Name*), alias (*Aliases*) i adresu
- krátké jméno (`srv2-fs`) doplní klient o **[[DNS přípona|DNS příponu]]** domény (z připojení do domény a z [[DHCP]] option 015) → proto na PC1-WIN funguje i `ping srv2-fs`

## Forwardery a kořenové nápovědy

Klient se ptá jen SRV1-DC. Jak ale server odpoví na `www.skola.cz`, o kterém nic neví?

1. podívá se do **svých zón a cache** – školní jména (`srv2-fs`, `ftp`) najde tady
2. když neumí odpovědět, pošle rekurzivní dotaz **forwarderu** (veřejný resolver nebo [[DNS]] poskytovatele), pokud je nastavený
3. když forwarder neodpoví nebo není nastavený, zeptá se přímo kořenových serverů přes **[[forwarder|root hints]]** a postupuje jako každý rekurzivní resolver

- forwardery se hodí, protože internet je často dostupný jen jednou cestou a forwarder má velkou cache → rychlé odpovědi
- **conditional forwarder** přeposílá jen dotazy na vybranou doménu (partnerská firma, jiný les)
- v Modulu 3 se nenastavují, ale vysvětlují, **proč mají klienti jako jediný [[DNS]] server řadič**; najdeš je v [[DNS]] Manageru → vlastnosti serveru → **Forwarders**

## Diagnostika

| Nástroj | Použití |
| :-- | :-- |
| **[[DNS]] Manager** | prohlédnout zóny a záznamy, zjistit, jestli záznam existuje a jakou má adresu |
| `nslookup <jméno> [server]` | dotaz; `nslookup -type=SRV _ldap._tcp.dc._msdcs.kotrba.cyberschool.internal` ověří [[SRV záznam\|SRV]] záznamy |
| `Resolve-DnsName <jméno>` | PowerShell – typ, [[DNS TTL\|TTL]] |
| `ipconfig /registerdns` | donutí klienta zapsat své záznamy znovu |
| `ipconfig /flushdns` | smaže cache klienta |
| `Clear-DnsServerCache` | smaže cache [[DNS]] serveru |
| `dcdiag /test:dns` | kontrola [[DNS]] na řadiči domény |

| Příznak | Pravděpodobná příčina | Řešení |
| :-- | :-- | :-- |
| `nslookup` na **jméno** → Non-existent domain | záznam chybí, překlep, klient se ptá jiného serveru | zkontrolovat zónu a [[DNS]] server na klientovi (`ipconfig /all`) |
| `nslookup` na **adresu** → Non-existent domain | chybí reverzní zóna nebo [[reverzní DNS\|PTR]] | založit reverzní zónu, doplnit [[reverzní DNS\|PTR]] |
| klient dostává starou adresu | záznam v cache klienta nebo serveru | `ipconfig /flushdns`, `Clear-DnsServerCache` |
| klient dostane adresu internetové karty serveru | v zóně je záznam i pro internetovou kartu | brát lokální záznam, nastavit [[DHCP]] |
| `ping` vyprší, ale `nslookup` vrací správnou adresu | server nepovoluje ping (firewall) | není chyba [[DNS]], ověřit službu jinak |
| `nslookup` neodpoví (timeout) | [[DNS]] neběží, špatná adresa serveru, blokovaný port 53 | zkontrolovat službu [[DNS]] Server a adresu na klientovi |

- v `nslookup` piš na konec jména **tečku** (`srv2-fs.kotrba.cyberschool.internal.`) → klient jméno nedoplňuje o další přípony; jinak se přes příponu Ethernet0 (`m-ta.cz`) může vrátit nesmyslná odpověď z internetu

## Bezpečnost

- zóny **integrované s [[AD DS|AD]]** a **Secure only** brání tomu, aby si kdokoli v síti zapsal vlastní záznam nebo přepsal cizí
- výchozí stav: **každý ověřený uživatel** smí vytvořit záznam A nebo [[reverzní DNS|PTR]], ale existující záznam jiného počítače nepřepíše; správu [[DNS]] mají jen členové skupiny **DnsAdmins** a správci domény
- **přenosy zón** povolit jen vybraným serverům – jinak by kdokoli získal celý seznam strojů
- [[DNS]] je tak spolehlivé jako řadič, na kterém běží → řadič je potřeba zálohovat

## U nás

- zóna `kotrba.cyberschool.internal` vznikla s [[AD DS]] jako integrovaná s [[AD DS|AD]] → zkontrolovat a doplnit **A** pro SRV2-FS a PC1-WIN
- **reverzní zóna** `16.168.192.in-addr.arpa` založená ručně, integrovaná s [[AD DS|AD]], Secure only, doplněný [[reverzní DNS|PTR]] pro SRV1-DC
- **alias** `ftp` → SRV2-FS
- klienti používají [[DNS]] SRV1-DC (`192.168.16.10`, z [[DHCP]])
- forwardery jen vysvětlujeme, nenastavujeme
