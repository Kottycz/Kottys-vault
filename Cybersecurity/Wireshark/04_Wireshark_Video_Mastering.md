# Wireshark – video Mastering Wireshark

YouTube: **Mastering Wireshark: The Complete Tutorial!** (Hacker Joe, ~55 min) – [odkaz](https://youtu.be/a_4MjV_-7Sw). Celkový přehled [[Wireshark|Wiresharku]] od instalace po analýzu TCP/UDP. Doplňuje místnosti [[01_Wireshark_Basics|Basics]], [[02_Wireshark_Packet_Operations|Packet Operations]] a [[03_Wireshark_Traffic_Analysis|Traffic Analysis]].

## Co Wireshark umí

- **zdarma**, běží na **Windows, Linux, macOS, Unix**
- zachytává data z **Ethernetu, Wi-Fi, Bluetooth** a dalších
- **živé zachytávání** paketů v reálném čase
- otevře data z jiných nástrojů – **tcpdump, WinDump, TShark**
- import a analýza **hex dumpů**
- export do **různých formátů**
- detailní analýza – protokoly, **filtry, barvy, hledání**
- **statistiky a grafy**
- **dešifrování** šifrovaných dat, pokud máš potřebné klíče

## Instalace a spuštění

- Windows / macOS – stáhnout z webu wireshark.org
- **Kali Linux** – je **předinstalovaný**
  - menu Applications → **Sniffing & Spoofing** → Wireshark
  - nebo terminál: `wireshark`
- po spuštění **vybrat rozhraní** (např. `wlan0`, `eth0`) – Wireshark sám ukáže aktivní rozhraní

## Rozhraní (GUI)

| Část | K čemu je |
| :-- | :-- |
| **Menu bar** | „velín" – všechny nástroje a volby |
| **Toolbar** | rychlé nástroje – stop, restart zachytávání, automatické posouvání |
| **Filter** | lišta pro filtry, např. `http` |
| **Packet List Pane** | seznam zachycených paketů |
| **Packet Details Pane** | obsah vybraného paketu – odkud, kam, protokoly („obsah obálky") |
| **Packet Bytes Pane** | **hex + ASCII** podoba dat |
| **Status bar** | počet paketů, délka zachytávání, profil |

### Proč nevidím žádné pakety?

1. v síti zrovna **neprobíhá provoz**
2. pakety **nejsou určené pro tvoje zařízení**
3. není zapnutý **[[promiskuitní režim]]** → Wireshark nezachytí všechen provoz

## První zachytávání

1. otevřít Wireshark → vybrat rozhraní
2. pro test otevřít prohlížeč a něco hledat → pakety se začnou objevovat
3. **uložit**: ikona Save → jméno souboru
   - výchozí formát **`.pcapng`**, jde i **`.pcap`** a další (viz [[PCAP]])

## Filtry

| | [[capture filter\|Capture filter]] | [[display filter\|Display filter]] |
| :-- | :-- | :-- |
| co dělá | zachytí jen některé pakety, **ostatní zahodí** | pakety jen **skryje**, nic nemaže |
| výhoda | šetří **výkon a paměť** | dá se kdykoli změnit |
| pozor | zahozené pakety **nejdou vrátit** | – |

- počet zobrazených paketů je ve **2. sloupci stavového řádku**
- doporučený tahák: **Wireshark cheat sheet od StationX**

### Příklady z videa

| Filtr | Co ukáže |
| :-- | :-- |
| `tcp` | jen [[TCP]] (web, přenosy souborů) |
| `udp` | jen [[UDP]] (video, VoIP) |
| `http` | jen [[HTTP]] |
| `ip.addr == 192.168.1.1` | komunikace s danou IP |
| `eth.addr == MAC` | pakety dané MAC adresy |
| `tcp.port == 80` | HTTP port |
| `udp.port == 53` | DNS |
| `tcp.port == 80 and ip.addr == 192.168.1.2` | **and** – obojí |
| `tcp.port == 443 or tcp.port == 80` | **or** – HTTPS nebo HTTP |
| `!(ip.addr == 192.168.1.100)` | **not** – vše kromě dané IP |

## Barvy (Coloring Rules)

- barvy = rychlé nalezení „jehly v kupce sena"
- výchozí pravidla: **View → Coloring Rules** (např. **Bad TCP** má vlastní barvu)
- vlastní pravidlo: **+** → filtr (např. `tcp.port == 80`) → název → barva

## Profily

- **vlastní nastavení** – capture/display filtry, čas, sloupce, protokoly, barvy
- dají se **importovat/exportovat** (kopírováním konfiguračních souborů)
- vytvoření: **pravý klik na Profile ve stavovém řádku → New** → jméno → OK
- změny platí **jen pro aktivní profil**

## Menu Statistics

| Funkce | Co ukáže |
| :-- | :-- |
| **Capture File Properties** | soubor (cesta, velikost, **hash**), čas prvního/posledního paketu, HW/OS/verze Wiresharku, rozhraní, počty paketů, průměry, **komentáře** |
| **Resolved Addresses** | IP/MAC přeložené na jména (DNS, [[ARP]]) |
| **Protocol Hierarchy** | **podíl protokolů** v %, bajty a pakety; pravý klik → Apply as Filter → Selected |
| **Conversations** | kdo s kým mluví a kolik; v IPv4 seřadit podle Packets → nahoře je „žrout" pásma; pravý klik → filtr A↔B |
| **Endpoints** | jednotlivá zařízení; záložky podle protokolu; Name resolution, export CSV, **mapa** |
| **Packet Lengths** | velikosti paketů – nezvykle velké/malé = možná **zahlcení, útok, porušení protokolu** |
| **I/O Graphs** | graf provozu v čase (osa X čas, Y pakety/tick); víc grafů s filtry (např. `udp` červeně) |
| **Service Response Time** | jak rychle služba odpovídá („stopky") |
| **DHCP (BOOTP)** | statistiky přidělování IP |
| **Flow Graph** | vizuální mapa toku mezi koncovými body – hledání úzkých míst |
| **HTTP / HTTP2** | statistiky webového provozu |
| **TCP Stream Graphs** | grafy jednoho TCP spojení (níže) |
| **UDP Multicast Streams** | jeden zdroj → skupina příjemců („rádio") |
| **IPv4 / IPv6 Statistics** | počty paketů a bajtů pro danou verzi IP |

- další méně běžné: ONC-RPC, 29West (finance), ANCP (broadband), **BACnet** (automatizace budov), **HART-IP** (průmysl), Sametime (IBM chat), Reliable Server Pooling, SOME/IP, DTP (Cisco trunking), F5

### TCP Stream Graphs

| Graf | Co ukazuje |
| :-- | :-- |
| **Time Sequence** | X = čas, Y = **sequence number**; čáry: data, ACK a **okno příjemce** (mezera = velikost okna) |
| **Throughput** | propustnost v B/s **jedním směrem** (I/O graf ukazuje oba) |
| **Round Trip Time** | čas od odeslání paketu po **ACK** |
| **Window Scaling** | jak se mění **velikost okna** během přenosu |

- prázdný graf → vybrat **jiný TCP paket**

## TCP analýza

### 3-way handshake ve Wiresharku

1. klient → **SYN**
2. server → **SYN, ACK**
3. klient → **ACK**
4. pak např. `HTTP GET`

Viz [[3-way handshake]].

### Follow Stream

- pravý klik → **Follow → TCP / UDP / HTTP Stream** (viz [[Follow Stream]])
- složí pakety do **čitelné podoby** (GET + odpověď serveru)
- HTTPS = nečitelný text (šifrování)
- volby: jen jedna strana / celá konverzace; formát **ASCII, EBCDIC, Hex Dump, C Arrays, Raw**
- **Save as** = uložit jako text; **Filter Out This Stream** = skrýt tento stream

### RST pakety

- server neběží → na každý **SYN** odpoví **RST** → spojení se nenaváže
- prohlížeče zkouší připojení **opakovaně** → víc párů SYN/RST
- velká **latence**: seřadit sloupec **Time** → velké mezery mezi pakety
- **port scan** (např. [[nmap]]): hodně šumu, zavřené porty odpovídají **RST**
- **žádný nástroj neodhalí vše automaticky** – nutná znalost a pozornost

## UDP analýza

- **bezspojový**, rychlý, **nespolehlivý** (ztracené pakety se znovu neposílají)
- bez navazování a ukončování spojení → **transaction oriented**
- používají ho **DHCP, DNS** a další

### DHCP

- server port **67**, klient port **68**
- délka paketu např. 308 B = **8 B UDP hlavička** + 300 B data
- po zapnutí zařízení: Discover / Offer / Request / ACK (+ Release)

### DNS

1. zachytávat → v prohlížeči otevřít doménu → stop
2. filtr `dns`
3. dotaz má **Transaction ID**, odpověď obsahuje **přeloženou IP**
4. v detailech rozbalit **Domain Name System**: query type, name, TTL, answer
5. flagy: **query/response, recursion desired, recursion available, response code**
6. Follow → **UDP Stream**
7. další záznamy: **NS, CNAME, MX, TXT**

## Související

[[Wireshark]] · [[Wireshark souhrn]] · [[PCAP]] · [[promiskuitní režim]] · [[capture filter]] · [[display filter]] · [[Follow Stream]] · [[Wireshark příkazy]] · [[Wireshark cvičení]] · [[01_Wireshark_Basics|Basics]] · [[02_Wireshark_Packet_Operations|Packet Operations]] · [[03_Wireshark_Traffic_Analysis|Traffic Analysis]]
