# Wireshark – přehled příkazů a zkratek

Tahák ze zápisů [[01_Wireshark_Basics|Basics]], [[02_Wireshark_Packet_Operations|Packet Operations]], [[03_Wireshark_Traffic_Analysis|Traffic Analysis]] a [[04_Wireshark_Video_Mastering|videa]]. Procvičení: [[Wireshark cvičení]].

## Klávesové zkratky

### Soubor a zachytávání

| Zkratka | Co dělá |
| :-- | :-- |
| `Ctrl+O` | otevřít soubor |
| `Ctrl+S` / `Ctrl+Shift+S` | uložit / uložit jako |
| `Ctrl+W` | zavřít soubor |
| `Ctrl+K` | **Capture Options** (rozhraní, capture filtr) |
| `Ctrl+E` | **start / stop** zachytávání |
| `Ctrl+R` | restart zachytávání / znovu načíst soubor |

### Pohyb mezi pakety

| Zkratka | Co dělá |
| :-- | :-- |
| `Ctrl+G` | **Go to Packet** (skok na číslo) |
| `Ctrl+Home` / `Ctrl+End` | první / poslední paket |
| `↑` `↓` | předchozí / další paket v seznamu |
| `Ctrl+↑` `Ctrl+↓` (`F7` `F8`) | předchozí / další paket i mimo seznam |
| `Ctrl+,` / `Ctrl+.` | předchozí / další paket **ve stejné konverzaci** |
| `Alt+←` / `Alt+→` | zpět / vpřed v historii |

### Hledání, označení, komentáře

| Zkratka | Co dělá |
| :-- | :-- |
| `Ctrl+F` | **Find Packet** (filtr / hex / string / regex) |
| `Ctrl+N` / `Ctrl+B` | najít další / předchozí |
| `Ctrl+M` | **označit / odznačit** paket |
| `Ctrl+Shift+M` / `Ctrl+Alt+M` | označit / odznačit všechny zobrazené |
| `Ctrl+Shift+N` / `Ctrl+Shift+B` | další / předchozí označený |
| `Ctrl+Alt+C` | **komentář** k paketu |
| `Ctrl+D` | ignorovat paket |
| `Ctrl+T` | nastavit časovou referenci |

### Analýza a zobrazení

| Zkratka | Co dělá |
| :-- | :-- |
| `Ctrl+/` | skok do **lišty filtru** |
| `Enter` | použít filtr |
| `Ctrl+Shift+I` | **Apply as Column** |
| `Ctrl+Shift+C` | zkopírovat pole **jako filtr** |
| `Ctrl+Alt+Shift+T` | **Follow TCP Stream** |
| `Ctrl+Alt+Shift+U` | **Follow UDP Stream** |
| `Ctrl+Alt+Shift+H` | **Follow HTTP Stream** |
| `Ctrl+→` / `Ctrl+←` | rozbalit / sbalit vše v detailech |
| `Shift+→` | rozbalit podstrom |
| `Ctrl++` / `Ctrl+-` / `Ctrl+=` | zvětšit / zmenšit / normální písmo |
| `Ctrl+Alt+1` | čas jako **datum a čas** |
| `Ctrl+Shift+P` | Preferences |
| `Ctrl+Shift+A` | Configuration Profiles |

## Důležitá menu

| Menu | K čemu |
| :-- | :-- |
| **File → Merge** | sloučit dva PCAP |
| **File → Export Specified Packets** | uložit jen vybrané pakety |
| **File → Export Objects → HTTP/SMB/TFTP/IMF/DICOM** | vytáhnout přenesené **soubory** |
| **Statistics → Capture File Properties** | hash, čas, komentář souboru, počty |
| **Statistics → Resolved Addresses** | IP ↔ DNS jména |
| **Statistics → Protocol Hierarchy** | podíl protokolů |
| **Statistics → Conversations** | kdo s kým (Ethernet, IPv4, IPv6, TCP, UDP) |
| **Statistics → Endpoints** | jednotlivá zařízení, Name resolution, GeoIP |
| **Statistics → IPv4 Statistics / DNS / HTTP** | detaily protokolů |
| **Statistics → I/O Graphs** | graf provozu v čase |
| **Statistics → Flow Graph** | tok mezi koncovými body |
| **Analyse → Expert Information** | varování a chyby ([[Expert Info]]) |
| **Analyse → Display Filter Expression** | průvodce stavbou filtru |
| **Analyse → Apply as Filter / Prepare as Filter** | filtr z pole |
| **Analyse → Conversation Filter** | jen pakety jedné konverzace |
| **View → Coloring Rules** | pravidla barev |
| **View → Colourise Conversation** | obarvit konverzaci |
| **View → Time Display Format** | formát času (UTC…) |
| **Edit → Preferences → Name Resolution** | překlad IP / portů, MaxMind GeoIP |
| **Edit → Preferences → Protocols → TLS** | soubor s klíči ([[SSLKEYLOGFILE]]) |
| **Edit → Configuration Profiles** | profily |
| **Tools → Credentials** | nešifrovaná jména a hesla (FTP, HTTP, IMAP, POP, SMTP) |
| **Tools → Firewall ACL Rules** | pravidla firewallu z paketu |

## Capture filtry (BPF)

| Filtr | Co zachytí |
| :-- | :-- |
| `host 10.10.10.5` | provoz s danou IP |
| `net 192.168.1.0/24` | celá podsíť |
| `src host 10.10.10.5` / `dst host …` | jen jedním směrem |
| `port 80` | port 80 (TCP i UDP) |
| `tcp port 80` | jen TCP port 80 |
| `portrange 20-25` | rozsah portů |
| `arp` / `icmp` / `udp` | jen daný protokol |
| `not port 22` | vše kromě SSH |
| `host 10.10.10.5 and tcp port 443` | kombinace |

## Display filtry

### Operátory

| Operátor | Význam | Příklad |
| :-- | :-- | :-- |
| `==` `eq` | rovná se | `ip.src == 10.10.10.100` |
| `!=` `ne` | nerovná se | `ip.src != 10.10.10.100` |
| `>` `gt` / `<` `lt` | větší / menší | `ip.ttl < 10` |
| `>=` `ge` / `<=` `le` | větší rovno / menší rovno | `ip.ttl <= 0xA` |
| `&&` `and` | a zároveň | `tcp.port == 80 and ip.addr == 10.0.0.2` |
| `\|\|` `or` | nebo | `tcp.port == 80 or tcp.port == 443` |
| `!` `not` | negace | `!(ip.addr == 10.0.0.100)` |
| `contains` | obsahuje (**case-sensitive**) | `http.server contains "Apache"` |
| `matches` | regex (**ne** case-sensitive) | `http.host matches "\\.(php\|html)"` |
| `in` | v seznamu | `tcp.port in {80,443,8080}` |
| `upper()` / `lower()` | velká / malá písmena | `lower(http.server) contains "apache"` |
| `string()` | převod na text | `string(frame.number) matches "[13579]$"` |

### Obecné

| Filtr | Co ukáže |
| :-- | :-- |
| `frame contains "text"` | text kdekoli v paketu |
| `frame.number == 100` | konkrétní paket |
| `frame.comment` | pakety s komentářem |
| `eth.addr == 00:11:22:33:44:55` | MAC adresa |
| `eth.src == …` / `eth.dst == …` | zdrojová / cílová MAC |
| `tcp.stream eq 5` | jeden TCP stream (to nastaví Follow Stream) |
| `tcp.analysis.flags` | TCP problémy (retransmise, dup ACK…) |

### IP, TCP, UDP

| Filtr | Co ukáže |
| :-- | :-- |
| `ip` | všechny IP pakety |
| `ip.addr == 10.10.10.111` | IP oběma směry |
| `ip.addr == 10.10.10.0/24` | podsíť |
| `ip.src == …` / `ip.dst == …` | zdroj / cíl |
| `ip.ttl < 10` | malé TTL |
| `tcp.port == 80` / `udp.port == 53` | port |
| `tcp.srcport == 1234` / `tcp.dstport == 80` | zdrojový / cílový port |
| `tcp.window_size <= 1024` | malé okno ([[SYN scan]]) |

### TCP flagy

| Filtr | Co ukáže |
| :-- | :-- |
| `tcp.flags == 2` | jen [[SYN]] |
| `tcp.flags == 18` | SYN + ACK |
| `tcp.flags == 16` | jen ACK |
| `tcp.flags == 4` | jen [[RST]] |
| `tcp.flags == 20` | RST + ACK |
| `tcp.flags == 1` | jen [[FIN]] |
| `tcp.flags.syn == 1` / `.ack` / `.reset` / `.fin` | flag nastaven (zbytek je jedno) |

- hodnoty: **FIN 1, SYN 2, RST 4, PSH 8, ACK 16, URG 32**

### Nmap skeny

| Filtr | Co odhalí |
| :-- | :-- |
| `tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size > 1024` | [[TCP connect scan]] (`-sT`) |
| `tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size <= 1024` | [[SYN scan]] (`-sS`) |
| `icmp.type==3 and icmp.code==3` | [[UDP scan]] – zavřené porty (`-sU`) |

### ARP

| Filtr | Co ukáže |
| :-- | :-- |
| `arp` | vše ARP |
| `arp.opcode == 1` / `arp.opcode == 2` | requesty / odpovědi |
| `arp.dst.hw_mac==00:00:00:00:00:00` | ARP scan |
| `arp.duplicate-address-detected or arp.duplicate-address-frame` | [[ARP poisoning]] |
| `arp.opcode == 1 && arp.src.hw_mac == MAC` | ARP flooding od MAC |

### DHCP, NetBIOS, Kerberos

| Filtr | Co ukáže |
| :-- | :-- |
| `dhcp` / `bootp` | vše DHCP |
| `dhcp.option.dhcp == 3` / `5` / `6` | Request / ACK / NAK |
| `dhcp.option.hostname contains "x"` | jméno hostitele |
| `dhcp.option.domain_name contains "x"` | doména |
| `nbns` / `nbns.name contains "x"` | NetBIOS |
| `kerberos` | vše Kerberos |
| `kerberos.CNameString and !(kerberos.CNameString contains "$")` | jen **uživatelé** (bez hostitelů) |
| `kerberos.realm contains ".org"` | doména tiketu |

### DNS a ICMP

| Filtr | Co ukáže |
| :-- | :-- |
| `dns` | vše DNS |
| `dns.flags.response == 0` / `== 1` | dotazy / odpovědi |
| `dns.qry.type == 1` | záznamy A |
| `dns.qry.name contains "x"` | dotaz na doménu |
| `dns.qry.name.len > 15 and !mdns` | dlouhé dotazy ([[DNS tunelování]]) |
| `dns contains "dnscat"` | nástroj dnscat |
| `icmp` | vše ICMP |
| `data.len > 64 and icmp` | velké ICMP ([[ICMP tunelování]]) |

### FTP

| Filtr | Co ukáže |
| :-- | :-- |
| `ftp` / `ftp-data` | příkazy / přenesená data |
| `ftp.request.command == "USER"` / `"PASS"` | jména / hesla |
| `ftp.response.code == 230` | úspěšné přihlášení |
| `ftp.response.code == 530` | **neúspěšné** přihlášení (bruteforce) |
| `(ftp.request.command == "PASS") and (ftp.request.arg == "password")` | password spray |

### HTTP a HTTPS

| Filtr | Co ukáže |
| :-- | :-- |
| `http` / `http2` | HTTP |
| `http.request` | všechny požadavky |
| `http.request.method == "GET"` / `"POST"` | metoda |
| `http.response.code == 404` | stavový kód |
| `http.request.uri contains "admin"` | URI |
| `http.host == "x"` / `http.server contains "x"` | host / server |
| `http.user_agent contains "sqlmap"` | podezřelý user-agent |
| `http.authorization` | hlavička Authorization (Basic Auth) |
| `data-text-lines contains "x"` | text od serveru |
| `(frame contains "jndi") or (frame contains "Exploit")` | Log4j |
| `tls` | vše TLS |
| `tls.handshake.type == 1` / `== 2` | Client Hello / Server Hello |
| `(http.request or tls.handshake.type == 1) and !(ssdp)` | kdo navazuje TLS |

## TShark (Wireshark v terminálu)

| Příkaz | Co dělá |
| :-- | :-- |
| `tshark -D` | seznam rozhraní |
| `tshark -i eth0` | zachytávat na `eth0` |
| `tshark -i eth0 -f "tcp port 80"` | s capture filtrem |
| `tshark -i eth0 -w zachyt.pcapng` | uložit do souboru |
| `tshark -r zachyt.pcapng` | přečíst soubor |
| `tshark -r zachyt.pcapng -Y "http.request"` | s display filtrem |
| `tshark -r zachyt.pcapng -q -z conv,ip` | IPv4 konverzace |
| `tshark -r zachyt.pcapng -q -z io,phs` | protocol hierarchy |
| `tshark -r zachyt.pcapng -q -z credentials` | nalezené přihlašovací údaje |
| `capinfos zachyt.pcapng` | info o souboru (hash, počet paketů) |

## Související

[[Wireshark]] · [[capture filter]] · [[display filter]] · [[Wireshark cvičení]] · [[Nmap příkazy]]
