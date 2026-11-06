# Wireshark – cvičení

Praktické procvičení k [[01_Wireshark_Basics|Basics]], [[02_Wireshark_Packet_Operations|Packet Operations]] a [[03_Wireshark_Traffic_Analysis|Traffic Analysis]]. Tahák: [[Wireshark příkazy]].

> [!tip] Interaktivní verze
> [Otevřít cvičení online](https://claude.ai/artifact/1jrpofEMRLKMVwyBnLiLDU) – odškrtávání, kontrola odpovědí a nápověda pod žárovkou.

## Zadání

- otevři ve Wiresharku soubor **`soubory/Wireshark_cviceni.pcapng`** (je ve stejné složce jako tento zápis)
- soubor je vyrobený na cvičení – malá domácí síť, ve které se odehrálo pár útoků
- odpovědi si piš do řádku **Odpověď:** a pošli je Claudovi ke kontrole
- **řešení je dole ve sbaleném bloku** – otevři ho až na konci
- IP a domény z útoků piš v **defanged** formátu (`10[.]0[.]0[.]1`), kde je to uvedeno

### Síť v souboru

| Zařízení | IP |
| :-- | :-- |
| brána / router / DNS | `192.168.50.1` |
| server | `192.168.50.10` |
| PC | `192.168.50.23` |
| ??? | `192.168.50.66` |

---

## Část A – Basics

1. Jaký **flag** je v komentáři celého souboru?
   Odpověď:
2. Kolik má soubor **celkem paketů**?
   Odpověď:
3. Jaké jsou **první 4 znaky** SHA256 hashe souboru?
   Odpověď:
4. Jaký je **komentář paketu číslo 100**?
   Odpověď:
5. Jdi na **paket 22**. Jaký **server** odpověděl (hlavička `Server`)? A jaká je hodnota **ETag**?
   Odpověď:
6. V bajtech paketů je schovaný text začínající `FLAG{prvni`. Jak celý zní?
   Odpověď:
7. Ze souboru jde **vyexportovat textový soubor** stažený přes HTTP. Jak se jmenuje a jaký flag je uvnitř?
   Odpověď:
8. Klikni na paket **20**, na řádek *Hypertext Transfer Protocol* a použij ho jako filtr. Jaký **dotaz** se objevil v liště a **kolik paketů** se zobrazilo?
   Odpověď:
9. Kolik **varování (Warnings)** ukazuje Expert Info?
   Odpověď:

## Část B – Packet Operations

10. Podle **Resolved Addresses**: jakou IP má `www.skola-test.cz`?
    Odpověď:
11. Kolik je **IPv4 konverzací**?
    Odpověď:
12. Která **dvojice IP** si vyměnila nejvíc paketů a kolik?
    Odpověď:
13. Zapni **Name resolution** v Endpoints (Ethernet). Jakého **výrobce** má MAC `08:00:27:be:ef:66`? A co z toho můžeš usoudit?
    Odpověď:
14. Kolik je v souboru **HTTP požadavků**, z toho **GET**, a kolik odpovědí **404**?
    Odpověď:
15. Kolik je **DNS dotazů** (ne odpovědí)?
    Odpověď:
16. Kolik paketů používá TCP porty **21, 22 nebo 80** (jedním filtrem)?
    Odpověď:
17. Kolik HTTP paketů má v user-agentu **Wfuzz**?
    Odpověď:

## Část C – Traffic Analysis

### Nmap

18. Kolik paketů odpovídá vzoru **SYN scanu**? Na jakou IP útočník skenoval?
    Odpověď:
19. Které **TCP porty** jsou na serveru **otevřené**?
    Odpověď:
20. Kolik je zpráv **„UDP port unreachable"**? Který skenovaný UDP port **neodpověděl**?
    Odpověď:

### ARP a MITM

21. Kolik **ARP requestů** vytvořil útočník? Za koho (jaké IP) se v ARP odpovědích vydává?
    Odpověď:
22. Přihlášení na web (**POST**): jaké je **číslo paketu**, jaké **jméno a heslo** a na jakou **cílovou MAC** paket ve skutečnosti šel?
    Odpověď:

### DHCP

23. Jaký **hostname** požádal o IP `192.168.50.41`? Jakou **MAC** má `KOTTY-PC`?
    Odpověď:

### FTP

24. Kolik je **neúspěšných přihlášení**? Jakým **jménem a heslem** se útočník nakonec přihlásil?
    Odpověď:
25. Jaký **soubor** útočník nahrál a jak se jmenuje **mimozemšťan** uvnitř?
    Odpověď:
26. Jakým **příkazem** změnil oprávnění souboru?
    Odpověď:

### HTTP

27. Kolik je **typů anomálních user-agentů**? Jaké je **číslo paketu** s překlepem v user-agentu?
    Odpověď:
28. Které **číslo paketu** obsahuje **HTTP Basic Auth** a jaké jméno:heslo v něm je?
    Odpověď:

### Tunelování

29. Jaká je **hlavní doména**, na kterou jdou podezřelé DNS dotazy (defanged)? Kolik je těch **dotazů**?
    Odpověď:
30. **Bonus:** subdomény jsou zakódované v **base32** (každá začíná dvouciferným pořadím `00`–`03`, to se vynechá). Co je v nich schované? *(CyberChef: From Base32)*
    Odpověď:
31. Jaký **protokol** je schovaný v **ICMP tunelu**, na jakou IP (defanged) a v jakém **čísle paketu** ho poprvé vidíš?
    Odpověď:

### Bonusy

32. Kolik záznamů ukáže **Tools → Credentials**?
    Odpověď:
33. Vyber **paket 467** a vytvoř pravidlo **IPFirewall (ipfw)**. Jaké je pravidlo pro **odepření zdrojové IPv4 adresy**?
    Odpověď:
34. Shrň útok vlastními slovy: kdo je útočník, co postupně udělal a co ukradl?
    Odpověď:

---

> [!success]- Řešení (otevři až na konci)
>
> | # | Odpověď | Jak na to |
> | :-- | :-- | :-- |
> | 1 | `FLAG{wireshark_start}` | Statistics → Capture File Properties |
> | 2 | `537` | stavový řádek / Capture File Properties |
> | 3 | `508f` (celý: `508f1af3c7aaa595c1278e81dc42e386a872ec43df4ca7b4d2f32622d60f1f7a`) | Capture File Properties |
> | 4 | `Tajna odpoved: KOMENTAR_NALEZEN_77` | `Ctrl+G` 100, nebo filtr `frame.comment` |
> | 5 | `Apache/2.4.41 (Ubuntu)`, ETag `"kotty-4815"` | detaily paketu → HTTP |
> | 6 | `FLAG{prvni_stream_nalezen}` | `Ctrl+F` → String → Packet bytes, nebo `frame contains "FLAG"` |
> | 7 | `zprava.txt` → `FLAG{export_objects_umim}` | File → Export Objects → HTTP |
> | 8 | `http`, `22` paketů | pravý klik → Apply as Filter → Selected |
> | 9 | `127` (103× RST, 24× duplicitní IP v ARP) | Analyse → Expert Information |
> | 10 | `203.0.113.80` | Statistics → Resolved Addresses |
> | 11 | `7` | Statistics → Conversations → IPv4 |
> | 12 | `192.168.50.66 ↔ 192.168.50.10`, `372` paketů | Conversations → seřadit Packets |
> | 13 | `PCSSystemtec` → **VirtualBox** virtuálka (typicky Kali útočníka) | Endpoints → Ethernet → Name resolution |
> | 14 | `11` požadavků, `10` GET, `4`× 404 | `http.request`, `http.request.method == "GET"`, `http.response.code == 404` |
> | 15 | `7` | `dns.flags.response == 0` |
> | 16 | `213` | `tcp.port in {21,22,80}` |
> | 17 | `2` | `http.user_agent contains "Wfuzz"` |
> | 18 | `103` paketů, cíl `192.168.50.10` | `tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size <= 1024` |
> | 19 | `21, 22, 80, 3306` (port 50000 není ze skenu – to je FTP data) | `tcp.flags == 18 and ip.src == 192.168.50.10` |
> | 20 | `5`, neodpověděl port `53` (open\|filtered) | `icmp.type==3 and icmp.code==3`, rozbalit ICMP → původní UDP |
> | 21 | `30` requestů; vydává se za **bránu `192.168.50.1`** (vůči PC) a za **PC `192.168.50.23`** (vůči bráně) | `arp.opcode == 1 && eth.src == 08:00:27:be:ef:66`, `arp.duplicate-address-detected` |
> | 22 | paket `437`, `kotty` / `Heslo123!`, cílová MAC `08:00:27:be:ef:66` = **útočník** (MITM) | `http.request.method == "POST"`, Apply as Column `eth.dst` |
> | 23 | `Galaxy-S23`, `00:1b:21:3a:4f:10` | `dhcp.option.dhcp == 3`, Option 12 a 50 |
> | 24 | `5`, `ftpuser` / `letmein` | `ftp.response.code == 530`, `ftp.request.command == "PASS"` |
> | 25 | `tajne.txt`, mimozemšťan `GLORP` | `ftp-data` → Follow TCP Stream |
> | 26 | `SITE CHMOD 777 tajne.txt` | `ftp.request.command` |
> | 27 | `4` typy (sqlmap, Nmap, Mozlila, Wfuzz), překlep v paketu `487` | `http.user_agent` → Apply as Column |
> | 28 | paket `457`, `admin:Wireshark2026` | `http.authorization` |
> | 29 | `exfil-data[.]net`, `4` dotazy | `dns.qry.name.len > 15 and !mdns` |
> | 30 | `uzivatel=kotty;heslo=Heslo123!;pc=KOTTY-PC;soubor=tajne.txt;konec` | spojit subdomény bez `00`–`03`, From Base32 |
> | 31 | `SSH`, `198[.]51[.]100[.]7`, paket `522` | `data.len > 64 and icmp`, `icmp contains "SSH"` |
> | 32 | `8` (7× FTP, 1× HTTP Basic Auth) | Tools → Credentials |
> | 33 | `add deny ip from 192.168.50.66 to any in` | Tools → Firewall ACL Rules → IPFirewall (ipfw) |
> | 34 | útočník `192.168.50.66` (VirtualBox): ARP scan sítě → SYN + UDP scan serveru → bruteforce FTP, nahrál `tajne.txt` a dal mu 777 → ARP poisoning mezi PC a bránou → odchytil přihlášení `kotty` a Basic Auth `admin` → web útoky (sqlmap, Wfuzz, Nmap NSE); z PC pak odchází data přes DNS a ICMP tunel | – |

## Související

[[Wireshark příkazy]] · [[01_Wireshark_Basics|Basics]] · [[02_Wireshark_Packet_Operations|Packet Operations]] · [[03_Wireshark_Traffic_Analysis|Traffic Analysis]] · [[04_Wireshark_Video_Mastering|Video]]
