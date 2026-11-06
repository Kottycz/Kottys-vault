# Protokoly a modely

## Pravidla – požadavky na síťový protokol

- Kódování zpráv
- Formátování a [[zapouzdření]] zpráv
- Velikost zprávy
- Načasování zpráv

## Načasování zpráv

- **Řízení toku** – definuje, kolik informací lze odeslat a jakou rychlostí mohou být doručeny.
- **Časový limit odpovědi** – protokoly určují, jak dlouho čekat na odpověď a jakou akci provést při vypršení limitu.
- **Metoda přístupu** – určuje, kdy může někdo odeslat zprávu.

## Možnosti doručování zpráv

- **[[unicast|Unicast]]** – informace se přenáší jedinému koncovému zařízení.
- **[[multicast|Multicast]]** – informace se přenáší jednomu nebo více koncovým zařízením.
- **[[broadcast|Broadcast]]** – informace se přenáší všem koncovým zařízením.

## Přehled síťových protokolů

Síťové protokoly definují společný formát a sadu pravidel pro výměnu zpráv mezi zařízeními.

- Síťové komunikační protokoly – [[TCP]]
- Zabezpečené síťové protokoly – [[TLS|SSL]], [[HTTPS]]
- Směrovací protokoly – [[OSPF]]

## Sady protokolů

### Aplikační vrstva

**Systém jmen:**
- [[DNS]] – systém doménových jmen.
- [[DHCP|DHCPv4]] – protokol dynamické konfigurace hostitele pro [[IPv4]], server dynamicky přiřazuje klientům adresy.

**E-mail:** [[SMTP]], [[POP3]], [[IMAP]].

**Přenos souborů:** [[FTP]], [[SFTP]], [[TFTP]].

**Web a webové služby:** [[HTTP]], [[HTTPS]], [[REST]].

### Transportní vrstva

**Orientované na spojení:**
- **[[TCP]]** – umožňuje spolehlivou komunikaci mezi procesy na samostatných hostitelích, poskytuje potvrzení přenosy potvrzující úspěšné doručení. Př.: email, web.

**Bez připojení:**
- **[[UDP]]** – umožňuje procesu na jednom hostiteli odesílat pakety procesu na jiném hostiteli, ale nepotvrzuje úspěšný přenos datagramu. Př.: streamování.

### Internetová vrstva

**Internetový protokol:**
- **[[IPv4]]** – přijímá segmenty z transportní vrstvy, balí zprávy do paketů a adresuje je pro end-to-end doručení. Používá 32bitovou adresu.
- **[[IPv6]]** – podobný IPv4, ale používá 128bitovou adresu.
- **[[NAT]]** – překlad síťových adres. Překládá IPv4 adresy z privátní sítě na globálně unikátní veřejné IPv4 adresy.

**Zprávy:**
- **[[ICMP|ICMPv4]]** – poskytuje zpětnou vazbu od cílového hostitele zdrojovému o chybách při doručování paketů.
- **[[ICMP|ICMPv6]]** – ICMP pro IPv6, podobná funkčnost jako ICMPv4.

**Směrovací protokoly:** [[OSPF]], [[EIGRP]], [[BGP]].

### Vrstva síťového přístupu

**Rozlišení adres:**
- **[[ARP]]** – poskytuje dynamické mapování mezi IPv4 adresou a hardwarovou adresou.

**Protokoly datového spojení:**
- **Ethernet** – definuje pravidla pro zapojení a signalizační standardy vrstvy přístupu k síti.
- **[[WLAN]]** – bezdrátová lokální síť, definuje pravidla pro bezdrátovou signalizaci na 2,4 GHz a 5 GHz.

## Standardizační organizace

- **[[IEEE]]** – Institut elektrotechnických a elektronických inženýrů, standardizuje síťová rozhraní (Ethernet, WLAN).
- **[[ISO]]** – International Organization for Standardization, mezinárodní normalizační organizace, vydala normu **ISO/IEC 7498** definující **referenční model [[OSI]]** (proto se model označuje i jako ISO/OSI).
- **[[IETF]]** – vydává internetové standardy ([[RFC]] dokumenty), stojí za sadou protokolů TCP/IP.

## Referenční modely

| [[OSI\|ISO/OSI Model]] (7 vrstev) | TCP/IP Protocol Suite (příklady) | TCP/IP Model (4 vrstvy) |
| :-- | :-- | :-- |
| Application (Aplikační) | [[HTTP]], [[DNS]], [[DHCP]], [[FTP]] | Application |
| Presentation (Prezentační) | (součást Application v TCP/IP) | Application |
| Session (Relační) | (součást Application v TCP/IP) | Application |
| Transport (Transportní) | [[TCP]], [[UDP]] | Transport |
| Network (Síťová) | [[IPv4]], [[IPv6]], [[ICMP\|ICMPv4]], [[ICMP\|ICMPv6]] | Internet |
| Data Link (Spojová) | Ethernet, [[WLAN]], [[SONET]], [[SONET\|SDH]] | Network Access |
| Physical (Fyzická) | (součást Network Access) | Network Access |

**ISO/OSI model** – vznikl jako obecný, výrobcem nezávislý referenční model (norma ISO/IEC 7498), popisuje síťovou komunikaci v 7 vrstvách. **TCP/IP model** je praktičtější, starší a skutečně používaná sada protokolů, má jen 4 vrstvy (horní tři vrstvy OSI slučuje do jedné aplikační vrstvy).

## Zapouzdření dat

- **Segmentace** – rozdělení na menší části.
- **Multiplexování** – technika umožňující přenášet víc signálů (datových toků) po jednom komunikačním kanálu zároveň.
- **Sekvencování** – označení zpráv čísly.

### Jednotky dat protokolu ([[PDU]])

| Vrstva ([[OSI]]) | PDU |
| :-- | :-- |
| Aplikační / Prezentační / Relační | **Data** – obecný termín pro PDU na aplikační vrstvě |
| Transportní | **Segment** |
| Síťová | **Paket** |
| Spojová | **Rámec (frame)** |
| Fyzická | **Bity** – PDU fyzické vrstvy při fyzickém přenosu dat přes médium |

## Data Access – adresy

Síťová a datová linková vrstva jsou zodpovědné za doručování dat ze zdrojového do cílového zařízení.

- **Zdrojové a cílové adresy síťové vrstvy** – zodpovídají za doručení IP paketu z původního zdroje do konečného cíle (ve stejné nebo vzdálené síti).
- **Zdrojové a cílové adresy datové vrstvy** – zodpovídají za doručení rámce z jedné síťové karty ([[NIC]]) do jiné NIC ve stejné síti.

### Logická adresa vrstvy 3

[[IP adresa]] je logická adresa síťové vrstvy pro doručení paketu z původního zdroje do konečného cíle.

- **Zdrojová IP adresa** – adresa odesílajícího zařízení (původní zdroj paketu).
- **Cílová IP adresa** – adresa přijímajícího zařízení (konečný cíl paketu).
- **Síťová část (IPv4) / předpona (IPv6)** – část adresy vlevo, označuje síť. Všechna zařízení ve stejné síti mají stejnou síťovou část.
- **Hostitelská část (IPv4) / ID rozhraní (IPv6)** – zbývající část, identifikuje konkrétní zařízení. Jedinečná pro každé zařízení/rozhraní.

**Zařízení ve stejné síti:** zdrojová IPv4 = PC1 `192.168.1.110`, cílová IPv4 = [[FTP]] server `192.168.1.9`.

**Zařízení ve vzdálené síti:** zdrojová IPv4 = PC1 `192.168.1.110`, cílová IPv4 = webový server `172.16.1.99`.
