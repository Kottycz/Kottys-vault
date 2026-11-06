# Wireshark – souhrn

Stručné shrnutí ze všech zápisů: [[01_Wireshark_Basics|Basics]] · [[02_Wireshark_Packet_Operations|Packet Operations]] · [[03_Wireshark_Traffic_Analysis|Traffic Analysis]] · [[04_Wireshark_Video_Mastering|Video]]. Detailní tahák: [[Wireshark příkazy]]. Procvičení: [[Wireshark cvičení]].

## Co to je

- **[[Wireshark]]** = zdarma, open-source **analyzátor paketů** (živý provoz i soubory [[PCAP]])
- **není [[IDS]]** – pakety jen čte, nic nemění ani sám nedetekuje
- použití: řešení problémů v síti, hledání útoků, učení protokolů
- `.pcapng` = výchozí formát (umí komentáře), `.pcap` = starší

## Rozhraní

| Část | K čemu |
| :-- | :-- |
| **Packet List** | seznam paketů (zdroj, cíl, protokol, info) |
| **Packet Details** | rozpis vrstev vybraného paketu |
| **Packet Bytes** | hex + ASCII |
| **Display Filter Bar** | filtry |
| **Status Bar** | počet paketů / zobrazených, profil |

- vrstvy v detailech: **Frame → Ethernet (MAC) → IP → TCP/UDP → aplikace (HTTP…)**
- nevidím pakety → není provoz / není pro mě / chybí [[promiskuitní režim]]

## Filtry

| | [[capture filter\|Capture]] | [[display filter\|Display]] |
| :-- | :-- | :-- |
| co dělá | uloží jen část provozu, zbytek **zahodí** | jen **skryje**, nic nemaže |
| kdy | před zachytáváním | kdykoli |
| příklad | `tcp port 80` | `tcp.port == 80` |

- operátory: `==` `!=` `>` `<` · `and` `or` `!` · `contains` · `matches` · `in {80,443}`
- lišta: **zelená** OK, **červená** chyba, **žlutá** nespolehlivé
- zlaté pravidlo: **na co jde kliknout, to jde filtrovat** (pravý klik → Apply as Filter)

## Nejdůležitější funkce

| Funkce | Co dělá |
| :-- | :-- |
| **Follow Stream** | složí konverzaci do čitelného textu ([[Follow Stream]]) |
| **Export Objects** | vytáhne přenesené soubory (HTTP, SMB, TFTP…) |
| **Expert Info** | varování a chyby ([[Expert Info]]) |
| **Conversation Filter** | jen pakety jedné konverzace |
| **Apply as Column** | z pole udělá sloupec |
| **Find Packet** `Ctrl+F` | hledání textu / hexu / regexu |
| **Mark** `Ctrl+M` / **Comment** | označení (zmizí) / komentář (zůstane v souboru) |
| **Profily** | uložená nastavení pro různé případy |

## Statistiky (menu Statistics)

- **Capture File Properties** – hash, čas, komentář, počty
- **Resolved Addresses** – IP ↔ jména
- **Protocol Hierarchy** – podíl protokolů
- **Conversations** – kdo s kým a kolik
- **Endpoints** – jednotlivá zařízení, výrobce MAC, GeoIP
- **DNS / HTTP / IPv4** – detaily protokolů, **I/O Graph** – provoz v čase

## Hledání útoků

| Útok | Jak ho poznám | Filtr |
| :-- | :-- | :-- |
| **TCP Connect scan** (`-sT`) | SYN, okno > 1024 | `tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size > 1024` |
| **SYN scan** (`-sS`) | SYN, okno ≤ 1024, odpověď RST | `… and tcp.window_size <= 1024` |
| **UDP scan** (`-sU`) | ICMP port unreachable = zavřený port | `icmp.type==3 and icmp.code==3` |
| **[[ARP poisoning]]** | dvě MAC pro jednu IP, záplava ARP | `arp.duplicate-address-detected` |
| **[[ICMP tunelování]]** | velké ICMP pakety | `data.len > 64 and icmp` |
| **[[DNS tunelování]]** | dlouhé divné subdomény | `dns.qry.name.len > 15 and !mdns` |
| **FTP bruteforce** | hodně neúspěšných přihlášení | `ftp.response.code == 530` |
| **Webové nástroje** | user-agent sqlmap, Nmap, Wfuzz, Nikto, překlepy | `http.user_agent contains "sqlmap"` |
| **Log4j** | POST s `jndi:ldap` | `frame contains "jndi"` |

## Identifikace hostitelů

- **DHCP** – hostname v Requestu (`dhcp.option.dhcp == 3`, Option 12)
- **NetBIOS** – jména stanic (`nbns`)
- **Kerberos** – uživatelé v `CNameString`, hodnoty s `$` = počítače

## HTTPS a hesla

- HTTPS je šifrované → dešifrovat jde jen se souborem klíčů [[SSLKEYLOGFILE]] (Edit → Preferences → Protocols → TLS)
- `tls.handshake.type == 1` = **Client Hello**, `== 2` = **Server Hello**
- **Tools → Credentials** – nešifrovaná hesla (FTP, HTTP, IMAP, POP, SMTP)
- **Tools → Firewall ACL Rules** – z paketu vytvoří pravidlo firewallu

## TCP a UDP v kostce

- **TCP** – spolehlivý, [[3-way handshake]]: **SYN → SYN/ACK → ACK**; RST = spojení odmítnuto
- **UDP** – bez spojení, rychlý, nespolehlivý; DNS (53), DHCP (67/68)
- flagy: **FIN 1, SYN 2, RST 4, PSH 8, ACK 16, URG 32**

## Související

[[Wireshark]] · [[Wireshark příkazy]] · [[Wireshark cvičení]] · [[nmap]]
