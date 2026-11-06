# Nmap – Live Host Discovery

TryHackMe: **FGP-Nmap Live Host Discovery** (první ze čtyř místností o Nmapu). Naučit se zjišťovat **živé hostitele** pomocí [[ARP]], [[ICMP]] a [[TCP]]/[[UDP]] pingu.

## Úvod

Při průzkumu sítě chceme zodpovědět dvě otázky:

1. **Které systémy v síti fungují?**
2. **Jaké služby na těchto systémech běží?**

Nástroj: **[[nmap|Nmap]]**. Tahle místnost řeší první otázku, druhou řeší další místnosti.

| # | Místnost | Téma |
| :-- | :-- | :-- |
| 1 | Nmap Live Host Discovery | které systémy jsou online |
| 2 | Nmap Basic Port Scans | základní skenování portů |
| 3 | Nmap Advanced Port Scans | pokročilé skenování portů |
| 4 | Nmap Post Port Scans | co po skenování portů |

**Proč zjišťovat živé hostitele dřív než porty:** skenovat porty na vypnutém systému jen ztrácí čas a dělá v síti zbytečný šum.

### Tři způsoby zjišťování živých hostitelů

1. **Kontrola [[ARP]]** – používá ARP request
2. **Kontrola [[ICMP]]** – používá ICMP request
3. **[[TCP]]/[[UDP]] ping scan** – posílá pakety na [[port|porty]] [[TCP]] a [[UDP]]

Dále se probírají dva skenery, které se s tím částečně překrývají: **[[arp-scan]]** a **[[masscan]]**.

### O Nmapu

- autor **Gordon Lyon (Fyodor)**, vydán v roce **1997**
- Nmap = **Network Mapper**, zdarma, open source, licence GPL
- průmyslový standard pro mapování sítí, hledání živých hostitelů a běžících služeb
- skriptovací stroj (NSE) umí navíc snímání otisků prstů i zneužívání zranitelností

### Kroky skenování v Nmapu

Skenování prochází kroky níže, mnohé jsou volitelné a závisí na argumentech příkazového řádku.

1. vyjmenovat cíle
2. **objevit živé hostitele** (téma této místnosti)
3. reverzní vyhledávání DNS ([[reverzní DNS]])
4. skenování portů
5. zjistit verze služeb
6. detekovat OS
7. traceroute
8. skripty
9. zápisový výstup

![[nmap_kroky_skenovani.png|450]]

## Podsítě

- **[[segment sítě|Segment sítě]]** = skupina počítačů propojených **sdíleným médiem** (např. ethernetový přepínač, WiFi přístupový bod). Odkazuje na **fyzické** připojení.
- **[[podsíť|Podsíť]]** = obvykle jeden nebo více segmentů spojených dohromady a nastavených na stejný router. Odkazuje na **logické** připojení.
- každá podsíť má vlastní rozsah IP adres a k větší síti se připojuje přes **router**
- v každé síti může být **[[firewall]]**, který vynucuje zásady zabezpečení

### Schéma ze zadání

Čtyři sítě (A, B/D, C) propojené přes cloud:

![[nmap_schema_siti.png|600]]

| Síť | Rozsah | Prefix |
| :-- | :-- | :-- |
| Network A | 10.1.100.0/24 | /24 |
| Network C | 10.3.200.0/24 | /24 |
| Network D | 10.4.0.0/16 | /16 |

Dvě sítě mají firewall (D a čtvrtá dole).

### Dva typy podsítí v zadání

| Prefix | Maska | Počet hostitelů |
| :-- | :-- | :-- |
| **/16** | `255.255.0.0` | asi 65 tisíc |
| **/24** | `255.255.255.0` | asi 253 |

Viz [[maska podsítě]] a [[délka prefixu]].

### ARP a podsítě

- při aktivním průzkumu chceme zjistit informace o skupině hostitelů nebo podsíti
- ve **stejné podsíti** skener spoléhá na dotazy **[[ARP]]** – cílem je zjistit MAC adresu, ale z odpovědi se pozná, že hostitel je **online**
- **ARP se nesměruje:** je to protokol **linkové vrstvy**, pakety ARP jsou vázány na svou podsíť a **neprojdou routerem**
- příklad: jsem v síti A → ARP najde jen zařízení v 10.1.100.0/24; ostatní pakety jdou přes výchozí bránu (router)
- tlačítko **View Site** spustí síťový simulátor, použije se v úkolech 2, 4 a 5

## Určení cílů

Před skenováním musím **specifikovat cíle**: seznam, rozsah IP adres nebo podsíť.

| Způsob | Zápis | Co prohledá |
| :-- | :-- | :-- |
| seznam | `MACHINE_IP scanme.nmap.org example.com` | 3 IP adresy |
| rozsah | `10.11.12.15-20` | 6 IP adres (.15 až .20) |
| podsíť | `MACHINE_IP/30` | 4 IP adresy |

Další možnosti:

- **vstupní soubor** se seznamem cílů: `nmap -iL list_of_hosts.txt`
- **kontrola seznamu bez skenování:** `nmap -sL TARGETS` – vypíše hostitele, které by Nmap skenoval; zkusí **reverzní DNS** všech cílů, jména mohou pentesterovi prozradit informace
- přepínač **`-n`** vypne dotazy na [[DNS]] server

## Vyhledání počítačů dostupných v síti

Využívají se protokoly vrstev **TCP/IP** (zdola nahoru):

- **[[ARP]]** z linkové vrstvy
- **[[ICMP]]** ze síťové vrstvy
- **[[TCP]]** z transportní vrstvy
- **[[UDP]]** z transportní vrstvy

| TCP/IP vrstva | Odpovídá OSI | Protokoly |
| :-- | :-- | :-- |
| aplikační | 7 aplikační, 6 prezentační, 5 relace | [[HTTP]], [[HTTPS]], [[SMTP]], [[POP3]], [[IMAP]], [[SSH]], [[FTP]], SNMP, [[Telnet]], RDP |
| transportní | 4 transportní | [[TCP]], [[UDP]] |
| síťová | 3 síťová | [[IPv4]], [[IPv6]], [[ICMP]], IPsec |
| odkazová | 2 datová linková, 1 fyzická | [[ARP]], Ethernet (802.3), WiFi (802.11), Bluetooth |

![[nmap_osi_tcpip.png|600]]

### Zopakování protokolů

- **[[ARP]]** má jediný účel: poslat **rámec na broadcast adresu** v segmentu sítě a požádat počítač s konkrétní IP, aby odpověděl svou **MAC adresou**
- **[[ICMP]]** má mnoho typů; **ICMP [[ping]]** ([[echo request]]) používá **Type 8 (Echo)** a **Type 0 (Echo Reply)**
- pokud pingnu systém ve **stejné podsíti**, před ICMP Echo předchází dotaz **[[ARP]]**
- **[[TCP]] a [[UDP]]** jsou protokoly transportní vrstvy; skener může poslat speciálně vytvořený paket na běžné porty TCP nebo UDP a ověřit, jestli cíl odpoví – účinné zvlášť, když je **ICMP Echo blokováno** (např. firewallem)

## Nmap Host Discovery s využitím ARP

Jak zjistit, kteří hostitelé jsou online? Je nezbytné **nepromarnit čas skenováním portů offline hostitele** nebo nepoužívané IP adresy.

### Co Nmap dělá ve výchozím nastavení

**Privilegovaný uživatel** = `root` nebo uživatel ze `sudoers`, který může spustit `sudo`.

| Kdo skenuje | Cíl | Co Nmap použije |
| :-- | :-- | :-- |
| privilegovaný | v **místní síti** (Ethernet) | požadavky **[[ARP]]** |
| privilegovaný | **mimo** místní síť | [[ICMP]] echo, [[TCP]] [[ACK]] na port 80, TCP [[SYN]] na port 443, ICMP požadavek na časové razítko |
| **neprivilegovaný** | mimo místní síť | **TCP [[3-way handshake]]** – SYN pakety na porty 80 a 443 |

- Nmap ve výchozím nastavení nejdřív **ping scan** a pak skenuje porty jen živých hostitelů
- jen zjistit živé hostitele **bez skenování portů**: `nmap -sn TARGETS` ([[ping scan]])

### Skenování ARP

- možné **jen ve stejné podsíti** jako cíl
- na Ethernetu (802.3) i WiFi (802.11) musím znát **MAC adresu** systému, se kterým chci komunikovat – je v hlavičce linkové vrstvy (zdrojová a cílová MAC)
- OS pošle **ARP REQUEST**; hostitel, který odpoví, je **aktivní**
- ARP funguje jen tehdy, je-li cíl ve stejné podsíti
- během skenování uvidím v síti **mnoho ARP dotazů**
- jen ARP bez skenování portů: **`nmap -PR -sn TARGETS`** (`-PR` = jen skenování ARP)

```
sudo nmap -PR -sn 10.10.210.6/24
```

![[nmap_PR_terminal.png|700]]

- výsledek: **256 IP adres, 4 hostitelé online** za 3,12 s; u každého je vidět i **MAC adresa**
- AttackBox měl IP 10.10.210.6 a skenoval podsíť /24

### Jak to vypadá v síti

1. Nmap pošle **ARP dotaz** na všechny cílové počítače
2. kdo je online, odpoví **ARP odpovědí** (reply)
3. stav: hostitel je aktivní

![[nmap_PR_diagram.png|650]]

V [[Wireshark|Wiresharku]] (nebo tcpdump) s filtrem `arp` je vidět:

- zdroj = **MAC adresa útočníkova AttackBoxu**
- cíl = **broadcast** (MAC cíle neznám)
- info: `Who has 10.10.210.1? Tell 10.10.210.6` – ptá se na **každou IP v podsíti** (.1, .2, .3, …)
- hostitel s dotazovanou IP odešle ARP odpověď se svou MAC adresou → je online

![[nmap_PR_wireshark.png|600]]

### arp-scan

[[arp-scan]] je skener postavený čistě na ARP dotazech, s mnoha možnostmi nastavení.

| Příkaz | Co dělá |
| :-- | :-- |
| `arp-scan --localnet` nebo `arp-scan -l` | ARP dotazy na **všechny platné IP adresy ve všech lokálních sítích** |
| `sudo arp-scan -I eth0 -l` | totéž, ale jen na rozhraní **eth0** (`-I` = rozhraní) |
| `sudo arp-scan 10.10.210.6/24` | prohledá zadanou podsíť |

- na AttackBoxu **není nainstalovaný**: `apt install arp-scan`
- výsledek: **256 hostitelů za 2,7 s, 3 odpověděli** – stejné tři živé cíle jako u `nmap -PR -sn` (Nmap navíc počítá sám sebe, proto 4)
- zachycené pakety jsou podobné jako u `nmap -PR -sn`

![[nmap_arpscan_terminal.png|700]]

![[nmap_arpscan.png|600]]

## Nmap Host Discovery s využitím ICMP

Můžu pingnout každou IP v cílové síti a zjistit, kdo odpoví: **ICMP Type 8 (Echo)** → odpověď **Type 0 (Echo Reply)**.

**Není to vždy spolehlivé:**

- mnoho **firewallů blokuje ICMP echo**
- nové verze Windows mají hostitelský firewall, který ICMP echo **standardně blokuje**
- ve stejné podsíti před ICMP požadavkem předchází dotaz ARP

### Tři druhy ICMP skenování

| Přepínač | Požadavek | Typ ICMP (dotaz → odpověď) | Příklad |
| :-- | :-- | :-- | :-- |
| **`-PE`** | ICMP echo | 8 → 0 | `nmap -PE -sn MACHINE_IP/24` |
| **`-PP`** | ICMP [[ICMP timestamp\|časové razítko]] | 13 → 14 | `nmap -PP -sn MACHINE_IP/24` |
| **`-PM`** | ICMP [[ICMP address mask\|maska adresy]] | 17 → 18 | `nmap -PM -sn MACHINE_IP/24` |

- **`-sn`** vždy přidat, pokud nechci následné skenování portů
- princip: pošle se požadavek a čeká se, že živý cíl odpoví

### Echo (`-PE`)

![[nmap_PE_diagram.png|650]]

**Ze stejné podsítě** (`sudo nmap -PE -sn 10.10.68.220/24`):

- **256 IP adres, 8 hostitelů online** za 2,11 s, vidět i MAC adresy
- Nmap **vůbec nemusel posílat ICMP** – hostitele potvrdil z **odpovědí ARP**
- MAC adresy cílů obvykle nevidím, pokud nejsem ve stejné podsíti

![[nmap_PE_terminal_stejna_podsit.png|700]]

**Z jiné podsítě** (zdroj 10.11.35.214 → cíl 10.10.68.0/24):

- stejných **8 hostitelů**, ale **bez MAC adres**, trvá to déle (**8,26 s**)
- Wireshark (filtr `icmp`): jedna zdrojová IP posílá `Echo (ping) request` na **všechny IP v cílové podsíti** (.1, .2, .3, …)

![[nmap_PE_terminal_jina_podsit.png|700]]

![[nmap_PE_wireshark_jina_podsit.png|600]]

### Časové razítko (`-PP`)

Používá se, když je **ICMP echo blokováno**.

![[nmap_PP_diagram.png|650]]

- požadavek na časové razítko (**Type 13**) → odpověď (**Type 14**)
- `sudo nmap -PP -sn 10.10.68.220/24` → **8 hostitelů online** za 10,93 s
- Wireshark: `Timestamp request` na všechny adresy v podsíti

![[nmap_PP_terminal.png|700]]

![[nmap_PP_wireshark.png|600]]

### Maska adresy (`-PM`)

![[nmap_PM_diagram.png|650]]

![[nmap_PM_terminal.png|700]]

- požadavek na masku adresy (**Type 17**) → odpověď (**Type 18**)
- `sudo nmap -PM -sn 10.10.68.220/24` → **0 hostitelů online** za 52,17 s
- přestože víme, že jich je aspoň osm, sken **nevrátil žádného**
- důvod: **firewall na trase blokuje tento typ ICMP paketů**
- sken přesto poslal požadavek na **všechny platné IP** a čekal na odpověď; **každý požadavek byl odeslán dvakrát** (to vidím ve Wireshark)

![[nmap_PM_wireshark.png|600]]

**Poučení:** když je blokován jeden typ paketu, vyberu jiný (echo → timestamp → address mask → TCP/UDP ping), abych síť a služby objevil.

## Nmap Host Discovery s využitím TCP a UDP (Task 7)

| Přepínač | Metoda | Co se pošle | Očekávaná odpověď živého cíle |
| :-- | :-- | :-- | :-- |
| **`-PS`** | [[TCP SYN ping]] | TCP paket s příznakem [[SYN]] (výchozí port **80**) | **SYN/ACK** (port otevřený) nebo **RST** (port zavřený) |
| **`-PA`** | [[TCP ACK ping]] | TCP paket s příznakem [[ACK]] (výchozí port **80**) | **RST** |
| **`-PU`** | [[UDP ping]] | UDP paket na (pravděpodobně zavřený) port | **ICMP Type 3, Code 3** (port nedostupný) |

- vždy s **`-sn`**, ať se neskenují porty
- porty lze zadat za přepínač: číslo (`-PS21`), rozsah (`-PS21-25`), seznam/kombinace (`-PS80,443,8080`)

### TCP SYN ping (`-PS`)

- pošle se paket se **SYN** na TCP port (standardně **80**) a čeká se na odpověď
- otevřený port odpoví **SYN/ACK**, zavřený **RST**
- zajímá mě **jen to, jestli nějaká odpověď přijde** – stav portu není podstatný, odpověď znamená, že hostitel je v provozu
- připomínka [[3-way handshake]]: **SYN → SYN/ACK → ACK**
- **privilegovaný uživatel** (root, sudo) může poslat SYN a **nemusí dokončit handshake**, i když je port otevřený
- **neprivilegovaný uživatel** nemá jinou možnost než **dokončit celý 3-way handshake**, pokud je port otevřený
- příklad: `sudo nmap -PS -sn 10.10.68.220/24` → **256 IP, 5 hostitelů online** za **17,38 s** (.52, .121, .125, .134, .220)
- Wireshark (filtr `!openvpn`): zdroj 10.11.35.214 posílá `[SYN]` na **port 80** všech IP v podsíti; žádné porty jsem nezadal, takže Nmap použil **80**

![[nmap_PS_handshake.png|600]]

![[nmap_PS_terminal.png|700]]

![[nmap_PS_wireshark.png|600]]

### TCP ACK ping (`-PA`)

- pošle **ACK** místo SYN → potřebuji **privilegovaného uživatele**
- jako **neprivilegovaný** se Nmap pokusí o 3-way handshake (tedy ACK nepošle)
- cíl odpoví **RST**, protože ACK **není součástí žádného probíhajícího spojení**; tato odpověď stačí ke zjištění, že je cíl aktivní
- výchozí port **80**, syntaxe jako u `-PS` (`-PA21`, `-PA21-25`, `-PA80,443,8080`)
- příklad: `sudo nmap -PA -sn 10.10.68.220/24` → **5 hostitelů online** za **29,89 s**
- Wireshark: spousta paketů `[ACK]` na port 80; **každý paket Nmap posílá dvakrát**
- systémy, které **nereagují**, jsou **offline nebo nepřístupné**

![[nmap_PA_diagram.png|650]]

![[nmap_PA_terminal.png|700]]

![[nmap_PA_wireshark.png|600]]

### UDP ping (`-PU`)

- na rozdíl od TCP SYN pingu se **neočekává odpověď**, když paket dorazí na **otevřený** UDP port (otevřený port mlčí)
- na **zavřený** UDP port cíl odpoví **ICMP Type 3, Code 3 (port nedostupný)** → to nepřímo ukáže, že je **cíl online**
- proto Nmap posílá UDP na **neobvyklý port**, který je téměř jistě zavřený (ve Wiresharku např. port **40125**, `Len=40`)
- příklad: `sudo nmap -PU -sn 10.10.68.220/24` → **5 hostitelů online** za **9,20 s** (nejrychlejší z těchto tří)
- syntaxe portů stejná jako u `-PS` / `-PA`

![[nmap_PU_diagram.png|600]]

![[nmap_PU_terminal.png|700]]

![[nmap_PU_wireshark.png|600]]

### Porovnání (stejná podsíť, stejných 5 hostitelů)

| Sken | Čas |
| :-- | :-- |
| `-PS` (SYN) | 17,38 s |
| `-PA` (ACK) | 29,89 s |
| `-PU` (UDP) | 9,20 s |

## Masscan (Task 7)

- používá **podobný přístup** k objevování dostupných systémů
- je **agresivní s rychlostí paketů**, aby sken skončil rychle
- přepínač `-p` + číslo portu / seznam / rozsah
- příklady:
  - `masscan MACHINE_IP/24 -p443`
  - `masscan MACHINE_IP/24 -p80,443`
  - `masscan MACHINE_IP/24 -p22-25`
  - `masscan MACHINE_IP/24 --top-ports 100`
- v AttackBoxu **není nainstalován** → `apt install masscan`

## Reverzní DNS (Task 8)

- výchozí chování Nmapu: **reverzní DNS jen pro online hostitele**
- názvy hostitelů mohou **prozradit hodně**, takže je to užitečný krok

| Volba | Co dělá |
| :-- | :-- |
| `-n` | **žádné** [[DNS]] dotazy (krok se přeskočí) |
| `-R` | reverzní DNS pro **všechny** hostitele, i offline |
| `--dns-servers DNS_SERVER` | použije **konkrétní DNS server** |

## Shrnutí (Task 9)

[[ARP]], [[ICMP]], [[TCP]] i [[UDP]] umožňují odhalit živého hostitele – **jakoukoli odpověď** bere Nmap jako důkaz, že je online.

| Typ skenu | Příklad příkazu |
| :-- | :-- |
| [[ARP]] | `sudo nmap -PR -sn MACHINE_IP/24` |
| [[ICMP]] Echo | `sudo nmap -PE -sn MACHINE_IP/24` |
| [[ICMP timestamp\|ICMP Timestamp]] | `sudo nmap -PP -sn MACHINE_IP/24` |
| [[ICMP address mask\|ICMP Address Mask]] | `sudo nmap -PM -sn MACHINE_IP/24` |
| [[TCP SYN ping]] | `sudo nmap -PS22,80,443 -sn MACHINE_IP/30` |
| [[TCP ACK ping]] | `sudo nmap -PA22,80,443 -sn MACHINE_IP/30` |
| [[UDP ping]] | `sudo nmap -PU53,161,162 -sn MACHINE_IP/30` |

- **`-sn`** přidat, pokud chci jen zjišťovat hostitele; bez něj Nmap po objevení **skenuje porty** živých hostitelů

| Volba | Účel |
| :-- | :-- |
| `-n` | žádné vyhledávání [[DNS]] |
| `-R` | zpětné vyhledávání DNS pro všechny hostitele (i offline) |
| `-sn` | pouze zjišťování hostitelů |

## Související

[[nmap]] · [[ping scan]] · [[TCP SYN ping]] · [[TCP ACK ping]] · [[UDP ping]] · [[SYN]] · [[RST]] · [[ACK]] · [[3-way handshake]] · [[TCP]] · [[UDP]] · [[ICMP timestamp]] · [[ICMP address mask]] · [[Wireshark]] · [[zjišťování živých hostitelů]] · [[arp-scan]] · [[masscan]] · [[segment sítě]] · [[podsíť]] · [[reverzní DNS]] · [[ARP]] · [[ICMP]] · [[ping]] · [[firewall]] · [[02_Nmap_Basic_Port_Scans|Basic Port Scans]] · [[03_Nmap_Advanced_Port_Scans|Advanced Port Scans]] · [[04_Nmap_Post_Port_Scans|Post Port Scans]]
