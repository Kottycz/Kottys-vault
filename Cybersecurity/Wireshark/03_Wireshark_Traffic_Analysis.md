# Wireshark – Traffic Analysis

TryHackMe: **FGP-Wireshark: Traffic Analysis** (třetí a poslední místnost). Hledání **anomálií a škodlivé aktivity** v provozu – spojení znalostí analytika a funkcí [[Wireshark|Wiresharku]].

## Úvod

| #   | Místnost                                                    | Téma                                   |
| :-- | :---------------------------------------------------------- | :------------------------------------- |
| 1   | [[01_Wireshark_Basics\|Wireshark Basics]]                   | GUI, disekce paketů, navigace, filtry  |
| 2   | [[02_Wireshark_Packet_Operations\|Packet Operations]]       | statistiky, filtry, operátory, funkce  |
| 3   | **Traffic Analysis**                                        | hledání útoků a anomálií v provozu     |

- cvičné soubory jsou ve VM v `Desktop/exercise-pcaps/…`
- **nikdy nekomunikovat** s doménami a IP z místnosti

## Nmap skeny

[[nmap|Nmap]] je standard pro mapování sítě → analytik musí poznat jeho **vzory v provozu**: [[TCP connect scan]], [[SYN scan]], [[UDP scan]].

### TCP flagy ve filtrech

| Co hledám | Přesně jen tyto flagy | Flag nastaven (zbytek je jedno) |
| :-- | :-- | :-- |
| jen [[SYN]] | `tcp.flags == 2` | `tcp.flags.syn == 1` |
| jen [[ACK]] | `tcp.flags == 16` | `tcp.flags.ack == 1` |
| SYN + ACK | `tcp.flags == 18` | `(tcp.flags.syn == 1) and (tcp.flags.ack == 1)` |
| jen [[RST]] | `tcp.flags == 4` | `tcp.flags.reset == 1` |
| RST + ACK | `tcp.flags == 20` | `(tcp.flags.reset == 1) and (tcp.flags.ack == 1)` |
| jen [[FIN]] | `tcp.flags == 1` | `tcp.flags.fin == 1` |

- čísla = součet bitů: **FIN 1, SYN 2, RST 4, PSH 8, ACK 16, URG 32**

### TCP Connect scan (`-sT`)

- **dokončí** [[3-way handshake]]
- používají ho uživatelé **bez root práv** (jiná možnost nemají)
- velikost okna obvykle **> 1024 bajtů** (čeká se přenos dat)

| Otevřený port | Zavřený port |
| :-- | :-- |
| SYN → / ← SYN,ACK / ACK → / RST,ACK → | SYN → / ← RST,ACK |

```
tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size > 1024
```

**Otevřený port**

![[ws_ta_connect_otevreny.png|650]]

**Zavřený port**

![[ws_ta_connect_zavreny.png|650]]

**Filtr**

![[ws_ta_connect_filtr.png|650]]

### SYN scan (`-sS`)

- handshake **nedokončí**
- vyžaduje **root**
- velikost okna obvykle **≤ 1024 bajtů**

| Otevřený port | Zavřený port |
| :-- | :-- |
| SYN → / ← SYN,ACK / RST → | SYN → / ← RST,ACK |

```
tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size <= 1024
```

**Otevřený port**

![[ws_ta_syn_otevreny.png|650]]

**Zavřený port**

![[ws_ta_syn_zavreny.png|650]]

**Filtr**

![[ws_ta_syn_filtr.png|650]]

### UDP scan (`-sU`)

- **bez handshaku**
- otevřený port → **žádná odpověď**
- zavřený port → [[ICMP]] **Type 3, Code 3** (Destination unreachable, Port unreachable)
- ICMP chyba v sobě nese **původní požadavek** (rozbalit sekci ICMP v detailech → je vidět, na jaký port šel)

```
icmp.type==3 and icmp.code==3
```

**Zavřený (69) a otevřený (68) port**

![[ws_ta_udp_porty.png|650]]

**ICMP nese původní požadavek**

![[ws_ta_udp_icmp_detail.png|450]]

**Filtr**

![[ws_ta_udp_filtr.png|650]]

## ARP Poisoning a Man In The Middle

- [[ARP]] přiřazuje **IP → MAC** v lokální síti
- **[[ARP poisoning]]** (ARP spoofing, MITM) = útočník posílá **falešné ARP odpovědi** (hlavně na bránu), přepíše tabulku IP↔MAC a **odposlouchává provoz** oběti

### ARP v kostce

- funguje jen v **lokální síti**, mezi MAC adresami
- **není zabezpečený**, **není směrovatelný**, **nemá ověřování**
- běžné vzory: request & response, oznámení, gratuitous pakety

| Filtr | Co hledá |
| :-- | :-- |
| `arp` | vše ARP |
| `arp.opcode == 1` | ARP **requesty** |
| `arp.opcode == 2` | ARP **odpovědi** |
| `arp.dst.hw_mac==00:00:00:00:00:00` | **ARP scan** |
| `arp.duplicate-address-detected or arp.duplicate-address-frame` | možný **ARP poisoning** |
| `((arp) && (arp.opcode == 1)) && (arp.src.hw_mac == target-mac-address)` | možné **ARP flooding** |

**Legitimní request a reply**

![[ws_ta_arp_legit.png|450]]

- podezřelé = **dvě různé ARP odpovědi** (konflikt) pro jednu IP → Expert Info varuje, ale ukáže jen **druhý výskyt**

### Postup vyšetřování (příklad z místnosti)

1. MAC končící `b4` oznámí IP `192.168.1.25`
2. dvě MAC adresy si nárokují `192.168.1.1` (brána) → **pokus o spoofing**
3. MAC `b4` posílá **záplavu ARP requestů** na celý rozsah `192.168.1.xxx` → **ARP flooding/scan**
4. HTTP provoz vypadá normálně na úrovni IP → přidat **MAC jako sloupec** (Apply as Column)
5. **všechny HTTP pakety jdou na MAC `b4`** → MITM potvrzen

**Konflikt – duplicitní IP**

![[ws_ta_arp_konflikt.png|650]]

**Záplava ARP requestů**

![[ws_ta_arp_flood.png|650]]

**HTTP provoz – na úrovni IP normální**

![[ws_ta_arp_http.png|650]]

**MAC jako sloupce – vše jde na „b4"**

![[ws_ta_arp_mac_sloupce.png|650]]

| Role | MAC | IP |
| :-- | :-- | :-- |
| **útočník** | `00:0c:29:e2:18:b4` | `192.168.1.25` |
| **brána** | `50:78:b3:f3:cd:f4` | `192.168.1.1` |
| **oběť** | `00:0c:29:98:c7:a8` | `192.168.1.12` |

- vždy si **zapisuj zjištění** během vyšetřování, pak je snazší je propojit

## Identifikace hostitelů: DHCP, NetBIOS, Kerberos

Kromě IP a MAC je potřeba poznat **jméno hostitele a uživatele** → výchozí bod vyšetřování.

### DHCP

- [[DHCP]] přiděluje IP konfiguraci; globálně: `dhcp` nebo `bootp`

| Typ | Filtr | Význam |
| :-- | :-- | :-- |
| **Request** | `dhcp.option.dhcp == 3` | obsahuje **hostname** |
| **ACK** | `dhcp.option.dhcp == 5` | potvrzený požadavek |
| **NAK** | `dhcp.option.dhcp == 6` | odmítnutý požadavek |

| Paket | Option | Význam |
| :-- | :-- | :-- |
| Request | **12** | Hostname |
| Request | **50** | požadovaná IP |
| Request | **51** | požadovaná doba pronájmu |
| Request | **61** | MAC klienta |
| ACK | **15** | název domény |
| ACK | **51** | přidělená doba pronájmu |
| NAK | **56** | zpráva – důvod zamítnutí (raději **číst**, ne filtrovat) |

```
dhcp.option.hostname contains "keyword"
dhcp.option.domain_name contains "keyword"
```

![[ws_ta_dhcp.png|650]]

### NetBIOS (NBNS)

- umožňuje komunikaci aplikací mezi hostiteli; globálně `nbns`
- dotazy obsahují **jméno, TTL a IP**

```
nbns.name contains "keyword"
```

![[ws_ta_nbns.png|650]]

### Kerberos

- výchozí **ověřování ve Windows doménách**; globálně `kerberos`
- **CNameString** = uživatelské jméno; hodnoty **končící `$` = jména hostitelů**

| Pole | Význam |
| :-- | :-- |
| `pvno` | verze protokolu |
| `realm` | doména pro tiket |
| `sname` | služba a doména tiketu |
| `addresses` | IP a NetBIOS jméno klienta (jen v requestech) |

```
kerberos.CNameString contains "keyword"
kerberos.CNameString and !(kerberos.CNameString contains "$")
kerberos.pvno == 5
kerberos.realm contains ".org"
kerberos.SNameString == "krbtg"
```

![[ws_ta_kerberos.png|450]]

## Tunelování: ICMP a DNS

- **tunelování** = zapouzdření dat do jiného protokolu, aby vypadala přirozeně
- útočníci ho zneužívají přes **důvěryhodné protokoly** (ICMP, DNS) k obejití ochrany → **exfiltrace dat** a **C2**

### ICMP tunel

- [[ICMP tunelování]] – data (TCP, HTTP, **SSH**) schovaná v **payloadu** ICMP
- indikátory: **velký objem** ICMP, **neobvyklá velikost** paketů (normál ~64 B)

```
icmp
data.len > 64 and icmp
```

![[ws_ta_icmp_tunel.png|650]]

### DNS tunel

- [[DNS tunelování]] – malware posílá dotazy na **subdomény**, které jsou ve skutečnosti **zakódované příkazy**: `encoded-commands.maliciousdomain.com`
- indikátory: **dlouhé** dotazy, divná jména, známé nástroje **dnscat**, **dns2tcp**, velký objem dotazů na jeden cíl

```
dns contains "dnscat"
dns.qry.name.len > 15 and !mdns
```

- `!mdns` = vyřadí místní dotazy zařízení (multicast DNS)

![[ws_ta_dns_tunel.png|450]]

## Cleartext protokoly: FTP

- FTP = jednoduchost, **ne bezpečnost** → MITM, krádež přihlašovacích údajů, phishing, malware, exfiltrace

| Série | Kód | Význam |
| :-- | :-- | :-- |
| x1x (info) | 211 / 212 / 213 | stav systému / adresáře / souboru |
| x2x (spojení) | 220 | služba připravena |
| | 227 / 228 / 229 | pasivní / dlouhý pasivní / rozšířený pasivní režim |
| x3x (ověření) | 230 / 231 | přihlášení / odhlášení |
| | 331 | platné uživatelské jméno |
| | 430 | neplatné jméno nebo heslo |
| | **530** | **nepřihlášen, špatné heslo** |
| | 200 | příkaz úspěšný |

| Příkaz | Význam |
| :-- | :-- |
| `USER` | uživatelské jméno |
| `PASS` | heslo |
| `CWD` | aktuální adresář |
| `LIST` | výpis |

```
ftp.response.code == 230
ftp.request.command == "USER"
ftp.request.command == "PASS"
ftp.request.arg == "password"
```

| Signál | Filtr |
| :-- | :-- |
| **bruteforce** – neúspěšná přihlášení | `ftp.response.code == 530` |
| **bruteforce** – cílové jméno | `(ftp.response.code == 530) and (ftp.response.arg contains "username")` |
| **password spray** – jedno heslo na víc účtů | `(ftp.request.command == "PASS") and (ftp.request.arg == "password")` |

![[ws_ta_ftp.png|450]]

## Cleartext protokoly: HTTP

- [[HTTP]] je nešifrovaný request-response protokol, perimetr ho **neblokuje** → phishing, webové útoky, exfiltrace, C2
- `http` / `http2` (HTTP2 = binární přenos, multiplexing)

| Filtr | Co ukáže |
| :-- | :-- |
| `http.request.method == "GET"` / `"POST"` | metody |
| `http.request` | všechny požadavky |
| `http.response.code == 200` | stavový kód |
| `http.user_agent contains "nmap"` | user-agent |
| `http.request.uri contains "admin"` | URI |
| `http.request.full_uri contains "admin"` | celé URI |
| `http.server contains "apache"` | server |
| `http.host contains "keyword"` / `http.host == "keyword"` | host |
| `http.connection == "Keep-Alive"` | stav spojení |
| `data-text-lines contains "keyword"` | čistý text od serveru |

| Kód | Význam |
| :-- | :-- |
| **200** | OK |
| **301 / 302** | přesunuto trvale / dočasně |
| **400** | špatný požadavek |
| **401** | potřeba přihlášení |
| **403** | zakázáno |
| **404** | nenalezeno |
| **405** | metoda nepovolena |
| **408** | timeout |
| **500** | interní chyba serveru |
| **503** | služba nedostupná |

### User-Agent

- útočníci ho umí upravit → **nikdy ho nedávat na whitelist**, je to jen doplňkový zdroj
- podezřelé:
  - **různé** user-agenty z jednoho hostitele v krátké době
  - nestandardní / vlastní hodnoty
  - **překlepy**: `Mozilla` ≠ `Mozlilla` ≠ `Mozlila`
  - nástroje **Nmap, Nikto, Wfuzz, sqlmap**
  - **payload** v user-agentu

```
(http.user_agent contains "sqlmap") or (http.user_agent contains "Nmap") or (http.user_agent contains "Wfuzz") or (http.user_agent contains "Nikto")
```

![[ws_ta_user_agent.png|450]]

### Log4j

- útok začíná **POST** požadavkem
- známé vzory: **`jndi:ldap`** a **`Exploit.class`**

```
http.request.method == "POST"
(ip contains "jndi") or (ip contains "Exploit")
(frame contains "jndi") or (frame contains "Exploit")
(http.user_agent contains "$") or (http.user_agent contains "==")
```

![[ws_ta_log4j.png|450]]

## Šifrované protokoly: dešifrování HTTPS

- **HTTPS** = HTTP přes **TLS** → bez klíčů obsah nevidíš (útočníci HTTPS používají taky)

| Filtr | Co ukáže |
| :-- | :-- |
| `http.request` | požadavky |
| `tls` | vše TLS |
| `tls.handshake.type == 1` | **Client Hello** |
| `tls.handshake.type == 2` | **Server Hello** |
| `ssdp` | SSDP (zjišťování služeb v síti) |

```
(http.request or tls.handshake.type == 1) and !(ssdp)
(http.request or tls.handshake.type == 2) and !(ssdp)
```

**Šifrovaný provoz, filtr http/http2 nic neukáže**

![[ws_ta_tls_sifrovane.png|450]]

**Client Hello / Server Hello**

![[ws_ta_tls_hello.png|450]]

- **soubor s klíči** ([[SSLKEYLOGFILE]]) = textový soubor s páry klíčů **pro každou relaci**
  - nastaví se proměnná prostředí `SSLKEYLOGFILE`, prohlížeč (**Chrome, Firefox**) tam klíče zapisuje
  - klíče se musí ukládat **během zachytávání**, zpětně je vytvořit nejde
- přidání: pravý klik nebo **Edit → Preferences → Protocols → TLS**
- po dešifrování jsou vidět formáty: Frame, Decrypted TLS, Decompressed Header, Reassembled TCP, Reassembled SSL

**Přidání klíčů – pravý klik**

![[ws_ta_keylog_pravy_klik.png|650]]

**Přidání klíčů – Edit → Preferences**

![[ws_ta_keylog_preferences.png|650]]

**Bez / s key log souborem**

![[ws_ta_keylog_s_bez.png|450]]

## Bonus: nešifrované přihlašovací údaje

- **Tools → Credentials** (od Wiresharku **3.1**)
- funguje pro **FTP, HTTP, IMAP, POP, SMTP**
- ukáže číslo paketu, protokol, jméno; kliknutím skočíš na paket s heslem/jménem
- **nespoléhat jen na to** – kontrolovat i ručně

![[ws_ta_credentials.png|450]]

## Bonus: akční výsledky (Firewall ACL)

- **Tools → Firewall ACL Rules** – z vybraného paketu vytvoří pravidla firewallu (IP, port, MAC)
- pravidla jsou pro **vnější rozhraní** firewallu
- podporuje: **iptables** (Netfilter), **Cisco IOS**, **ipfilter**, **ipfw**, **pf**, **Windows Firewall (netsh)**

![[ws_ta_firewall_acl.png|450]]

## Otázky z místnosti

| Úkol | Otázka | Odpověď |
| :-- | :-- | :-- |
| Nmap | počet TCP Connect skenů | `1000` |
| | typ skenu na TCP port 80 | `TCP Connect` |
| | počet „UDP close port" zpráv | `1083` |
| | otevřený UDP port v rozsahu 55–70 | `68` |
| ARP | ARP requesty útočníka | `284` |
| | HTTP pakety přijaté útočníkem | `90` |
| | počet zachycených jmen a hesel | `6` |
| | heslo „Client986" | `clientnothere!` |
| | komentář „Client354" | `Nice work!` |
| DHCP/NBNS/Kerberos | MAC „Galaxy A30" | `9a:81:41:cb:96:6c` |
| | NetBIOS registrace „LIVALJM" | `16` |
| | kdo chtěl IP `172.16.13.85` | `Galaxy-A12` |
| | IP uživatele „u5" | `10[.]1[.]12[.]2` |
| | hostname v Kerberos | `xp1$` |
| Tunel | protokol v ICMP tunelu | `SSH` |
| | hlavní doména DNS tunelu | `dataexfil[.]com` |
| FTP | neúspěšná přihlášení | `737` |
| | velikost souboru účtu „ftp" | `39424` |
| | nahraný soubor | `resume.doc` |
| | příkaz pro práva | `CHMOD 777` |
| HTTP | počet anomálních user-agentů | `6` |
| | paket s překlepem v user-agentu | `52` |
| | začátek útoku Log4j – paket | `444` |
| | IP z dekódovaného base64 | `62[.]210[.]130[.]250` |
| HTTPS | Client Hello na accounts.google.com – rámec | `16` |
| | počet HTTP2 paketů po dešifrování | `115` |
| | authority hlavička rámce 322 | `safebrowsing[.]googleapis[.]com` |
| | flag | `FLAG{THM-PACKETMASTER}` |
| Credentials | paket s HTTP Basic Auth | `237` |
| | paket s prázdným heslem | `170` |
| Firewall | ipfw – deny source IPv4 (paket 99) | `add deny ip from 10.121.70.151 to any in` |
| | ipfw – allow destination MAC (paket 231) | `add allow MAC 00:d0:59:aa:af:80 any in` |

- **defanged** formát = tečky v hranatých závorkách (`10[.]1[.]12[.]2`), aby adresa nešla omylem otevřít

## Související

[[Wireshark]] · [[Wireshark souhrn]] · [[ARP poisoning]] · [[DNS tunelování]] · [[ICMP tunelování]] · [[SSLKEYLOGFILE]] · [[SYN scan]] · [[TCP connect scan]] · [[UDP scan]] · [[nmap]] · [[Wireshark příkazy]] · [[Wireshark cvičení]] · [[01_Wireshark_Basics|Basics]] · [[02_Wireshark_Packet_Operations|Packet Operations]]
