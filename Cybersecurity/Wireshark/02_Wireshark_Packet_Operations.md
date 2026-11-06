# Wireshark – Packet Operations

TryHackMe: **MTA-Wireshark: Packet Operations** (druhá ze tří místností). Pokročilé funkce [[Wireshark|Wiresharku]]: **statistiky**, **filtry**, **operátory** a **funkce**.

## Úvod

| #   | Místnost                                                    | Téma                                   |
| :-- | :---------------------------------------------------------- | :------------------------------------- |
| 1   | [[01_Wireshark_Basics\|Wireshark Basics]]                   | GUI, disekce paketů, navigace, filtry  |
| 2   | **Packet Operations**                                       | statistiky, filtry, operátory, funkce  |
| 3   | [[03_Wireshark_Traffic_Analysis\|Traffic Analysis]]         | hledání útoků a anomálií v provozu     |

- soubor: `Exercise.pcapng`
- **nikdy nekomunikovat** s doménami a IP z místnosti – jsou jen pro referenci

## Statistiky | Souhrn

Menu **Statistics** – celkový obraz provozu (rozsah, protokoly, koncové body, konverzace) → z toho si analytik dělá **hypotézu** pro vyšetřování.

| Funkce | Co ukáže | Menu |
| :-- | :-- | :-- |
| **Resolved Addresses** | IP adresy a jejich **DNS jména** (bere se z DNS odpovědí v souboru) | Statistics → Resolved Addresses |
| **Protocol Hierarchy** | **strom protokolů** s počty paketů a procenty; pravým klikem jde filtrovat | Statistics → Protocol Hierarchy |
| **Conversations** | provoz **mezi dvěma koncovými body**; záložky Ethernet, IPv4, IPv6, TCP, UDP | Statistics → Conversations |
| **Endpoints** | **jedinečné** koncové body (jedno pole) – Ethernet, IPv4, IPv6, TCP, UDP | Statistics → Endpoints |

**Resolved Addresses**

![[ws_ops_resolved_addresses.png|650]]

**Protocol Hierarchy**

![[ws_ops_protocol_hierarchy.png|650]]

**Conversations**

![[ws_ops_conversations.png|450]]

**Endpoints**

![[ws_ops_endpoints.png|650]]

### Překlad jmen (Name Resolution)

- **MAC → výrobce**: podle **prvních 3 bajtů** MAC (OUI od IEEE), jen u známých výrobců
  - v Endpoints → tlačítko **Name resolution** vlevo dole
- **IP a porty → jména**: standardně **vypnuto**, zapnout přes **Edit → Preferences → Name Resolution**
- po zapnutí jsou jména vidět v Packet List, Conversations i Endpoints

**Edit → Preferences → Name Resolution**

![[ws_ops_name_resolution_nastaveni.png|450]]

**Endpoints bez / s překladem jmen**

![[ws_ops_endpoints_name_resolution.png|650]]

### GeoIP

- mapování IP adres na **mapu/místo** (město, organizace)
- standardně **vypnuto**, potřebuje databázi **MaxMind**
- cesta: **Edit → Preferences → Name Resolution → MaxMind database directories**
- mapa potřebuje **internet** (lab VM ho nemá)

**GeoIP v detailech paketu**

![[ws_ops_geoip_nastaveni.png|450]]

**Endpoints s GeoIP a mapou**

![[ws_ops_endpoints_geoip.png|650]]

## Statistiky | Detaily protokolů

| Funkce | Co ukáže | Menu |
| :-- | :-- | :-- |
| **IPv4 / IPv6 Statistics** | statistiky jen pro **jednu verzi IP** | Statistics → IPvX Statistics |
| **DNS** | rozpis DNS paketů – **rcode, opcode, class, query type**, statistiky služeb a dotazů | Statistics → DNS |
| **HTTP** | rozpis HTTP – **kódy požadavků a odpovědí**, původní požadavky | Statistics → HTTP |

**IPv4 Statistics**

![[ws_ops_ipv4_statistics.png|450]]

**DNS**

![[ws_ops_dns_statistics.png|650]]

**HTTP**

![[ws_ops_http_statistics.png|450]]

## Filtrování paketů | Principy

| | [[capture filter\|Capture filter]] | [[display filter\|Display filter]] |
| :-- | :-- | :-- |
| účel | uloží jen **část provozu** | ukáže jen **část paketů** (nic nemaže) |
| kdy | nastaví se **před** zachytáváním, během něj **nejde měnit** | dá se měnit **kdykoli** |
| syntaxe | BPF – hex, bajtové posuny, boolean | protokol.pole, ~3000 protokolů |
| příklad port 80 | `tcp port 80` | `tcp.port == 80` |
| nápověda | **Capture → Capture Filters** | **Analyse → Display Filters** |

- syntaxe **nejsou zaměnitelné** – display filtr nejde použít jako capture filtr a naopak
- běžná praxe: **zachytit vše** a pak filtrovat display filtrem; capture filtry jen zkušení (co nezachytíš, už nemáš)

### Syntaxe capture filtrů

- **Scope:** `host`, `net`, `port`, `portrange`
- **Direction:** `src`, `dst`, `src or dst`, `src and dst`
- **Protocol:** `ether`, `wlan`, `ip`, `ip6`, `arp`, `rarp`, `tcp`, `udp`

**Capture → Capture Filters**

![[ws_ops_capture_filters.png|450]]

**Analyse → Display Filters**

![[ws_ops_display_filters.png|450]]

### Porovnávací operátory

| English | C-like | Význam | Příklad |
| :-- | :-- | :-- | :-- |
| `eq` | `==` | rovná se | `ip.src == 10.10.10.100` |
| `ne` | `!=` | nerovná se | `ip.src != 10.10.10.100` |
| `gt` | `>` | větší | `ip.ttl > 250` |
| `lt` | `<` | menší | `ip.ttl < 10` |
| `ge` | `>=` | větší nebo rovno | `ip.ttl >= 0xFA` |
| `le` | `<=` | menší nebo rovno | `ip.ttl <= 0xA` |

- funguje **desítkově i hexadecimálně**

### Logické výrazy

| English | C-like | Význam | Příklad |
| :-- | :-- | :-- | :-- |
| `and` | `&&` | a zároveň | `(ip.src == 10.10.10.100) and (ip.src == 10.10.10.111)` |
| `or` | `\|\|` | nebo | `(ip.src == 10.10.10.100) or (ip.src == 10.10.10.111)` |
| `not` | `!` | negace | `!(ip.src == 10.10.10.222)` |

> [!tip] Místo `!= hodnota` používej `!(pole == hodnota)` – `!=` je zastaralé a může dávat špatné výsledky.

### Lišta filtru (Packet Filter Toolbar)

- filtry se píšou **malými písmeny**
- **automatické doplňování**, části protokolu se oddělují **tečkou** (`ip.src`, `tcp.port`)
- barva lišty:

| Barva | Význam |
| :-- | :-- |
| **zelená** | platný filtr |
| **červená** | neplatný filtr |
| **žlutá** | funguje, ale je **nespolehlivý** → raději přepsat |

**Barvy lišty**

![[ws_ops_filtr_barvy.png|650]]

**Funkce lišty filtru**

![[ws_ops_filtr_toolbar.png|650]]

## Filtrování paketů | Filtry protokolů

### IP filtry (L3)

| Filtr | Co ukáže |
| :-- | :-- |
| `ip` | všechny IP pakety |
| `ip.addr == 10.10.10.111` | pakety s touto IP (**bez ohledu na směr**) |
| `ip.addr == 10.10.10.0/24` | pakety z podsítě |
| `ip.src == 10.10.10.111` | pakety **odeslané z** IP |
| `ip.dst == 10.10.10.111` | pakety **poslané na** IP |

- `ip.addr` = **oba směry**, `ip.src` / `ip.dst` = **konkrétní směr**

![[ws_ops_ip_filtry.png|650]]

### TCP a UDP filtry (L4)

| Filtr | Co ukáže |
| :-- | :-- |
| `tcp.port == 80` | TCP s portem 80 |
| `udp.port == 53` | UDP s portem 53 |
| `tcp.srcport == 1234` | TCP ze zdrojového portu 1234 |
| `udp.srcport == 1234` | UDP ze zdrojového portu 1234 |
| `tcp.dstport == 80` | TCP na cílový port 80 |
| `udp.dstport == 5353` | UDP na cílový port 5353 |

![[ws_ops_tcp_udp_filtry.png|650]]

### Aplikační filtry – HTTP a DNS (L7)

| Filtr | Co ukáže |
| :-- | :-- |
| `http` | všechny HTTP pakety |
| `http.response.code == 200` | HTTP odpovědi s kódem 200 |
| `http.request.method == "GET"` | HTTP GET požadavky |
| `http.request.method == "POST"` | HTTP POST požadavky |
| `dns` | všechny DNS pakety |
| `dns.flags.response == 0` | **DNS dotazy** |
| `dns.flags.response == 1` | **DNS odpovědi** |
| `dns.qry.type == 1` | DNS záznamy typu **A** |

![[ws_ops_http_dns_filtry.png|650]]

### Display Filter Expression

- **Analyse → Display Filter Expression** – průvodce stavbou filtru
- ukáže **všechna pole** protokolu, typ hodnoty (číslo / řetězec) a předdefinované hodnoty
- hodí se, když si nepamatuješ název pole

![[ws_ops_display_filter_expression.png|450]]

## Pokročilé filtrování

| Filtr | Typ | Co dělá | Příklad |
| :-- | :-- | :-- | :-- |
| `contains` | porovnání | hledá hodnotu v poli; **rozlišuje velikost písmen** | `http.server contains "Apache"` |
| `matches` | porovnání | hledá **regex**; **nerozlišuje** velikost písmen | `http.host matches "\\.(php\|html)"` |
| `in` | množina | hodnota je v **seznamu** | `tcp.port in {80,443,8080}` |
| `upper` | funkce | převede na **VELKÁ** písmena | `upper(http.server) contains "APACHE"` |
| `lower` | funkce | převede na **malá** písmena | `lower(http.server) contains "apache"` |
| `string` | funkce | převede ne-řetězec na **řetězec** | `string(frame.number) matches "[13579]$"` |

**contains**

![[ws_ops_contains.png|450]]

**matches**

![[ws_ops_matches.png|450]]

**in**

![[ws_ops_in.png|450]]

**upper**

![[ws_ops_upper.png|450]]

**lower**

![[ws_ops_lower.png|450]]

**string**

![[ws_ops_string.png|450]]

> [!note] Rozdíly ve Wiresharku 4.x (ověřeno na 4.2)
> - v množině se píšou **čárky**: `tcp.port in {80,443,8080}` – verze s mezerami hází chybu
> - zpětné lomítko v regexu se **zdvojuje**: `http.host matches "\\.(php|html)"` – s jedním `\.` hází chybu

### Záložky, tlačítka, profily

- **záložky filtrů** – uložené oblíbené/složité filtry (ikona vlevo v liště filtru)
- **tlačítka filtrů** – filtr na **jedno kliknutí** (tlačítko `+` vpravo v liště)
- **profily** – různá nastavení (barvy, tlačítka, sloupce) pro různé případy
  - **Edit → Configuration Profiles** nebo **vpravo dole ve stavovém řádku → Profile**

**Záložky**

![[ws_ops_zalozky.png|450]]

**Tlačítka filtrů**

![[ws_ops_tlacitka_filtru.png|450]]

**Profily**

![[ws_ops_profily.png|450]]

## Otázky z místnosti (Exercise.pcapng)

| Otázka | Odpověď |
| :-- | :-- |
| IP hostitele začínajícího na „bbc" | `199.232.24.81` |
| počet IPv4 konverzací | `435` |
| bajtů (k) z MAC „Micro-St" | `7474` |
| počet IP spojených s „Kansas City" | `4` |
| IP organizace „Blicnet" | `188.246.82.7` |
| nejpoužívanější cílová IPv4 | `10.100.1.33` |
| max. doba požadavku na službu DNS | `0.467897` |
| počet HTTP požadavků na `rad[.]msn[.]com` | `39` |
| počet IP paketů | `81420` |
| pakety s TTL < 10 | `66` |
| pakety s TCP portem 4444 | `632` |
| HTTP GET na port 80 | `527` |
| DNS dotazy typu A | `51` |
| IIS servery – pakety ne z portu 80 | `21` |
| IIS servery – verze 7.5 | `71` |
| pakety s porty 3333, 4444, 9999 | `2235` |
| pakety se **sudým** TTL | `77289` |
| profil „Checksum Control" – Bad TCP Checksum | `34185` |
| existující tlačítko filtru – zobrazené pakety | `261` |

### Filtry k otázkám

- IP paketů: `ip`
- TTL < 10: `ip.ttl < 10`
- port 4444: `tcp.port == 4444`
- porty: `tcp.port in {3333,4444,9999}`
- sudé TTL: `string(ip.ttl) matches "[02468]$"`

## Související

[[Wireshark]] · [[Wireshark souhrn]] · [[capture filter]] · [[display filter]] · [[Wireshark příkazy]] · [[Wireshark cvičení]] · [[01_Wireshark_Basics|Basics]] · [[03_Wireshark_Traffic_Analysis|Traffic Analysis]]
