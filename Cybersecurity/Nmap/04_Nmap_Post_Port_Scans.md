# Nmap – Post Port Scans

TryHackMe: **MTA-Nmap Post Port Scans** (čtvrtá, poslední místnost o Nmapu). Co dělat **po** [[skenování portů|skenování portů]]: zjistit verze služeb, operační systém, trasu, spustit skripty a uložit výstup.

## Úvod

- v předchozích místnostech: vyjmenování cílů, **živí hostitelé** ([[01_Nmap_Live_Host_Discovery]]), [[reverzní DNS]], **[[skenování portů]]** ([[02_Nmap_Basic_Port_Scans]], [[03_Nmap_Advanced_Port_Scans]])
- tato místnost se zaměřuje na **kroky 5–9** a na to, jak je provést po skenování portů

![[nmap_kroky_skenovani.png|600]]

| Krok | Co |
| :-- | :-- |
| 5 | zjistit **verze služeb** ([[detekce služeb]]) |
| 6 | detekovat **OS** ([[detekce OS]]) |
| 7 | **[[traceroute]]** |
| 8 | **skripty** ([[NSE]]) |
| 9 | **uložit výstup** ([[výstupní formáty Nmap]]) |

## Detekce služeb (`-sV`)

- po zjištění otevřených portů chceme vědět, **jaký software** na nich běží a v **jaké verzi** (verze → známé zranitelnosti)
- spuštění: **`-sV`**
- `-sV` **dokončí [[3-way handshake]]** → **stealth scan (`-sS`) není s `-sV` možný**
- v tabulce přibyde sloupec **VERSION**, např. `22/tcp open ssh OpenSSH 6.7p1 Debian 5+deb8u8 (protocol 2.0)`, banner `nginx 1.6.2`
- intenzita zjišťování: **`--version-intensity LEVEL`**, od **0** (nejlehčí) do **9** (nejúplnější)
  - **`--version-light`** = intenzita **2**
  - **`--version-all`** = intenzita **9**

Příklad (`sudo nmap -sV MACHINE_IP`):

![[post_terminal_sV.png|650]]

- 995 zavřených portů, 5 otevřených s verzemi: **OpenSSH 6.7p1**, **Postfix smtpd**, **nginx 1.6.2**, **Dovecot pop3d**, **rpcbind 2-4**
- `Service Info`: host `debra2.thm.local`, OS: Linux, CPE `cpe:/o:linux:linux_kernel`
- trvání 8,40 s (výrazně déle než samotný sken)

## Detekce OS (`-O`) a Traceroute

### Detekce OS (`-O`)

- spuštění: **`-O`** (velké O), typicky `nmap -sS -O MACHINE_IP`
- Nmap odhadne OS podle chování TCP/IP zásobníku

![[post_terminal_O.png|650]]

- výsledek: `Device type: general purpose`, `Running: Linux 3.X`, `OS CPE: cpe:/o:linux:linux_kernel:3.13`, `OS details: Linux 3.13`, `Network Distance: 1 hop`

**Přesnost:**

- jádro 3.16 určil přesně; **Fedora s jádrem 5.13.14** označil jako **2.6.X** → **OS správně, verze špatně**
- potřebuje alespoň **1 otevřený a 1 uzavřený [[port]]**
- **virtualizace** výsledek zkresluje
- bere to jako odhad, ne jistotu

### Traceroute (`--traceroute`)

- zjistí **trasu** (směrovače) k cíli
- Nmap začíná s **vysokým [[TTL]] a snižuje** ho; klasický `traceroute`/`tracert` začíná **nízkým TTL a zvyšuje** ho
- příklad: `nmap -sS --traceroute MACHINE_IP`

![[post_terminal_traceroute.png|650]]

- žádné směrovače → cíl je **přímo připojený** (1 [[hop]], RTT 1,48 ms)
- hodně routerů je nastaveno, aby **neodesílaly [[ICMP]] Time-to-Live exceeded** → trasa pak nemusí být vidět ([[ICMP]])

## Nmap Scripting Engine (NSE)

- **skript** = kód spouštěný bez kompilace
- Nmap podporuje skripty v jazyce [[Lua jazyk|Lua]]; **[[NSE]]** je interpret Lua
- skriptů je téměř **600**, leží v `/usr/share/nmap/scripts`; kolem **130** jich začíná `http`

![[post_terminal_ls_http.png|650]]

- spouštění: **`--script=default`** nebo zkratka **`-sC`**
- **kategorie skriptů:**


| Kategorie | Popis |
| :-- | :-- |
| `auth` | související s autentizací |
| `broadcast` | objev hostitelů pomocí [[broadcast]] zpráv |
| `brute` | **brute-force** audit hesel proti přihlášení |
| `default` | výchozí, stejné jako `-sC` |
| `discovery` | získání informací (tabulky databází, názvy [[DNS]]) |
| `dos` | detekce serverů zranitelných vůči **DoS** |
| `exploit` | pokusy o **zneužití** zranitelných služeb |
| `external` | kontroly třetích stran (Geoplugin, Virustotal) |
| `fuzzer` | fuzzing útoky |
| `intrusive` | intruzivní ([[brute force]], exploity) |
| `malware` | hledá zadní vrátka |
| `safe` | bezpečné, cíl nepoškodí |
| `version` | zjištění verzí služeb |
| `vuln` | kontrola zranitelností nebo jejich zneužití |

- některé skripty jsou ve **více kategoriích**
- **opatrně** u `brute`, `dos`, `exploit`, `intrusive` – mohou cíl poškodit nebo být nezákonné bez povolení

### Výchozí skripty (`-sC`)

- `sudo nmap -sS -sC MACHINE_IP` – po [[SYN]] skenu spustí výchozí skripty

![[post_terminal_sC.png|650]]

- **22 [[SSH]]:** `ssh-hostkey` – 4 veřejné klíče (DSA 1024, RSA 2048, ECDSA 256, EdDSA 256)
- **25 [[SMTP]]:** `smtp-commands`, `ssl-cert` (platnost 2021-08-10 až 2031-08-08)
- **80 [[HTTP]]:** `http-title` – „Welcome to nginx on Debian!"
- **110** `pop3-capabilities`, **111** `rpcinfo`, **143** `imap-capabilities`

### Konkrétní skript (`--script`)

- `--script "SCRIPT-NAME"` nebo vzor: `--script "ftp*"` (zahrne i `ftp-brute`!)
- skript si lze přečíst (`less`, textový editor)
- `ftp-brute` = brute-force audit hesel proti [[FTP]]
- `http-date` = získá **datum a čas** z HTTP serveru
- příklad: `sudo nmap -sS -n --script "http-date" MACHINE_IP`

![[post_terminal_http_date.png|650]]

- výstup: `http-date: Fri, 10 Sep 2021 07:04:26 GMT; 0s from local time`
- **pozor:** vlastní skripty nebo skripty stažené z internetu = **riziko**; nespouštět od autora, kterému nevěříš

## Ukládání výstupů

Tři užitečné formáty + čtvrtý nedoporučený:

| Formát | Volba | Použití |
| :-- | :-- | :-- |
| **Normal** | `-oN FILENAME` | čitelný jako na obrazovce |
| **Grepable** | `-oG FILENAME` | snadné `grep`ování, 1 řádek na hostitele |
| **XML** | `-oX FILENAME` | nejlepší pro zpracování jinými programy |
| **Všechny tři** | `-oA FILENAME` | `-oN` + `-oG` + `-oX` |
| **Script Kiddie** | `-oS FILENAME` | leetspeak, nedoporučeno |

### Normal (`-oN`)

- `nmap -sS -sV -O -oN MACHINE_IP_scan MACHINE_IP`

![[post_terminal_oN.png|650]]

### Grepable (`-oG`)

- `grep` = **G**lobal **R**egular Expression **P**rinter
- normální výstup má 21 řádků, grepable jen 4

![[post_terminal_oG.png|650]]

- `grep http MACHINE_IP_scan.nmap` → jen `80/tcp open http nginx 1.6.2` (bez IP)

![[post_terminal_grep_nmap.png|650]]

- `grep http MACHINE_IP_scan.gnmap` → celý řádek **včetně IP**

![[post_terminal_grep_gnmap.png|650]]

→ grepable se hodí, když potřebuješ u výsledku **IP hostitele**.

### Script Kiddie (`-oS`)

- `nmap -sS 127.0.0.1 -oS FILENAME`

![[post_terminal_kiddie.png|650]]

- výstup typu „`$tart!ng nMaP 7.60 ( httpz://nMap.0rG )`" – jen pro zábavu

## Shrnutí


| Volba | Význam |
| :-- | :-- |
| `-sV` | informace o službě/verzi na otevřených portech |
| `-sV --version-light` | nejpravděpodobnější sondy (2) |
| `-sV --version-all` | všechny sondy (9) |
| `-O` | [[detekce OS]] |
| `--traceroute` | trasa k cíli |
| `--script=SCRIPTS` | spuštění skriptů |
| `-sC` / `--script=default` | výchozí skripty |
| **`-A`** | zkratka: `-sV -O -sC --traceroute` |
| `-oN` | normální výstup |
| `-oG` | grepable výstup |
| `-oX` | XML výstup |
| `-oA` | normální + XML + grepable |

## Související

[[nmap]] · [[detekce služeb]] · [[detekce OS]] · [[NSE]] · [[Lua jazyk]] · [[výstupní formáty Nmap]] · [[skenování portů]] · [[SYN scan]] · [[3-way handshake]] · [[ICMP]] · [[Nmap příkazy]] · [[01_Nmap_Live_Host_Discovery|Live Host Discovery]] · [[02_Nmap_Basic_Port_Scans|Basic Port Scans]] · [[03_Nmap_Advanced_Port_Scans|Advanced Port Scans]]
