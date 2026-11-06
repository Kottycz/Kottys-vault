# Nmap – Basic Port Scans

TryHackMe: **MTA-Nmap Basic Port Scans** (druhá ze čtyř místností o Nmapu, součást modulu Úvod do síťové bezpečnosti). Naučit se **[[skenování portů|skenovat porty]]**: [[TCP connect scan|TCP connect]], [[SYN scan|TCP SYN]] a [[UDP scan|UDP]].

## Úvod

| #   | Místnost                                                  | Téma                         |
| :-- | :-------------------------------------------------------- | :--------------------------- |
| 1   | [[01_Nmap_Live_Host_Discovery\|Nmap Live Host Discovery]] | které systémy jsou online    |
| 2   | **Nmap Basic Port Scans**                                 | základní [[skenování portů]] |
| 3   | [[03_Nmap_Advanced_Port_Scans\|Nmap Advanced Port Scans]] | pokročilé skenování portů    |
| 4   | [[04_Nmap_Post_Port_Scans\|Nmap Post Port Scans]]         | co po skenování portů        |

- v předchozí místnosti se řešilo **objevování online systémů**
- dosud tři kroky skenování [[nmap|Nmapu]]: **vyjmenovat cíle**, **objevit živé hostitele**, **zpětné vyhledávání [[DNS]]** ([[reverzní DNS]])
- další krok: **které porty jsou otevřené a naslouchají a které jsou zavřené**
- tato místnost vysvětluje:
  1. skenování portů [[TCP]]
  2. skenování portů [[TCP]] [[SYN]]
  3. skenování portů [[UDP]]
- navíc: **specifikace portů**, **rychlost skenování** a **počet paralelních sond**

### Kroky skenování v Nmapu

Skenování portů je **4. krok**.

![[nmap_kroky_skenovani.png|450]]

## Porty

- **[[port|Port]]** ([[TCP]] nebo [[UDP]]) identifikuje **síťovou službu** běžící na hostiteli, stejně jako [[IP adresa]] identifikuje hostitele v síti
- **server** poskytuje síťovou službu a dodržuje konkrétní **protokol** (např. poskytování času, odpovědi na dotazy [[DNS]], poskytování webových stránek)
- [[port]] se obvykle spojuje se službou přes **číslo portu**
  - [[HTTP]] server se standardně váže na **TCP port 80**
  - pokud podporuje SSL/[[TLS]], naslouchá na **TCP portu 443**
  - 80 a 443 jsou **výchozí porty** pro [[HTTP]] a [[HTTPS]], administrátor může zvolit jiná čísla
- na jakémkoli TCP nebo UDP portu (na stejné IP adrese) může naslouchat **nejvýše jedna služba**

### Stavy portů

**Zjednodušeně** má port dva stavy:

1. **otevřený** = na portu naslouchá nějaká služba
2. **uzavřený** = na portu nenaslouchá žádná služba

V praxi se musí počítat s [[firewall|firewallem]] (port může být otevřený, ale pakety blokuje brána). Proto Nmap zvažuje **šest stavů** (viz [[stavy portů]]):

| Stav | Význam |
| :-- | :-- |
| **Open** | služba naslouchá na zadaném portu |
| **Closed** | na portu nenaslouchá žádná služba, ale port je **přístupný** (dosažitelný, není blokován firewallem ani jinými zařízeními) |
| **Filtered** | Nmap **nemůže určit**, zda je port otevřený nebo zavřený, protože port **není přístupný** (obvykle [[firewall]]); pakety Nmapu nebo odpovědi jsou blokovány |
| **Unfiltered** | Nmap **nemůže určit**, zda je port otevřený nebo zavřený, ačkoli je přístupný; stav se vyskytuje při použití [[ACK scan\|skenování ACK]] (`-sA`) |
| **Open\|Filtered** | Nmap nemůže určit, zda je port **otevřený nebo filtrovaný** |
| **Closed\|Filtered** | Nmap nemůže rozhodnout, zda je port **uzavřen nebo filtrován** |

## TCP flagy

- Nmap podporuje různé typy skenování [[TCP]] portů
- aby šel pochopit rozdíl mezi nimi, je potřeba znát **[[hlavička TCP|hlavičku TCP]]**
- [[hlavička TCP]] je **prvních 24 bajtů TCP segmentu** (definováno v [[RFC]] 793)
  - **1. řádek:** číslo zdrojového a cílového portu (každé **16 bitů = 2 bajty**)
  - **2. a 3. řádek:** pořadové číslo segmentu a číslo potvrzení
  - každý řádek má **32 bitů (4 bajty)**, celkem **šest řádků = 24 bajtů**

![[ps_tcp_hlavicka.png|600]]

Nejdůležitější jsou **příznaky (flagy)**, které Nmap může nastavit nebo zrušit. Nastavení příznakového bitu = nastavení jeho hodnoty na **1**. Zleva doprava:

1. **[[URG]]** – urgentní příznak; ukazatel naléhavosti je významný, data jsou naléhavá a segment se zpracuje **okamžitě**, aniž by se čekalo na dříve odeslané segmenty
2. **[[ACK]]** – příznak potvrzení; číslo potvrzení je významné, slouží k **potvrzení příjmu** segmentu TCP
3. **[[PSH]]** – push; žádá TCP, aby data **okamžitě předal aplikaci**
4. **[[RST]]** – reset; slouží k **resetování připojení** (např. [[firewall]] jej odešle k přerušení spojení; také když jsou data odeslána hostiteli a na přijímací straně není služba, která by odpověděla)
5. **[[SYN]]** – synchronizace; zahajuje **třícestné navázání spojení TCP** a synchronizuje pořadová čísla (měla by být nastavena náhodně)
6. **[[FIN]]** – odesílatel již nemá žádná data k odeslání

## TCP Connect Scan (`-sT`)

- funguje **dokončením [[3-way handshake]]**
- při standardním navazování spojení klient odešle segment s příznakem **[[SYN]]**, server odpoví **SYN/ACK**, pokud je [[port]] otevřený, a klient handshake dokončí **[[ACK]]**

![[nmap_PS_handshake.png|500]]

- zajímá nás jen to, **zda je port otevřený**, ne navazování spojení, proto se spojení hned přeruší **RST/ACK**
- spuštění: **`-sT`**

![[ps_diagram_sT.png|600]]

- pokud **nejsi privilegovaný uživatel** (root nebo sudo), je kontrola připojení [[TCP]] **jediná možnost**, jak zjistit otevřené TCP porty

### Wireshark

- Nmap posílá pakety **SYN** na různé porty (256, 443, 143 …)
- ve výchozím nastavení se zkouší **1000 nejběžnějších portů**
- **uzavřený** port odpoví **RST/ACK** (signalizuje, že není otevřený); vzor se opakuje pro všechny uzavřené porty

![[ps_wireshark_sT.png|700]]

- port **143 je otevřený**: odpověděl SYN/ACK a Nmap dokončil handshake odesláním ACK; čtvrtý paket spojení rozbije **RST/ACK**

![[ps_wireshark_sT_143.png|700]]

### Příklad

```
nmap -sT MACHINE_IP
```

![[ps_terminal_sT.png|650]]

- **`-F`** = rychlý režim, snížení počtu skenovaných portů z 1000 na **100** nejběžnějších
- **`-r`** = porty se skenují **v po sobě jdoucím pořadí** místo náhodného (užitečné, když se porty otevírají konzistentním způsobem, např. při spouštění cíle)

## TCP SYN Scan (`-sS`)

- **výchozí režim** [[skenování portů]] v Nmapu, vyžaduje **privilegovaného uživatele** (root nebo sudo)
- **nedokončí [[3-way handshake]]**: jakmile obdrží odpověď od serveru, spojení přeruší
- protože se spojení nenavázalo, **snižuje se pravděpodobnost, že bude skenování zaprotokolováno** cílem
- spuštění: **`-sS`**

![[ps_diagram_sS.png|600]]

- [[Wireshark]]: u uzavřených portů je chování podobné jako u [[TCP]] connect (RST/ACK); u otevřeného portu (25, 80) přijde SYN/ACK a Nmap odpoví **[[RST]]**

![[ps_wireshark_sS.png|700]]

### Rozdíl mezi `-sT` a `-sS`

- **nahoře `-sT`:** otevřený [[port]] 80 vyžaduje, aby Nmap **dokončil 3-way handshake** ([[SYN]] → SYN/ACK → [[ACK]]) a až pak spojení ukončil RST/ACK
- **dole `-sS`:** nemusí handshake dokončit; Nmap pošle **RST**, jakmile přijme SYN/ACK

![[ps_wireshark_sT_vs_sS.png|700]]

### Příklad

```
sudo nmap -sS MACHINE_IP
```

![[ps_terminal_sS.png|650]]

- úspěšně objeví otevřené porty z dřívějšího skenování TCP connect, ale **cíl skenování nezaprotokoloval**
- spolehlivá volba při spuštění jako root nebo přes sudo

## UDP Scan (`-sU`)

- **[[UDP]] je protokol bez spojení**, proto nevyžaduje **žádný handshake**
- nelze zaručit, že služba naslouchající na [[UDP]] portu bude reagovat na naše pakety
- pokud je UDP paket odeslán na **uzavřený [[port]]**, vrátí se chyba nedostupnosti portu **[[ICMP]] (typ 3, kód 3)**
- spuštění: **`-sU`**; lze zkombinovat s jiným [[TCP]] skenem
- na **otevřený** UDP port **nemůžeme čekat žádnou odpověď** → odeslání UDP paketu na otevřený port nám nic neřekne

![[ps_diagram_sU_otevreny.png|600]]

- očekáváme paket **[[ICMP]] typu 3, cíl nedostupný, kód 3 (port nedostupný)**
- **porty UDP, které negenerují žádnou odpověď, Nmap uvede jako otevřené**

![[ps_diagram_sU_uzavreny.png|600]]

- každý uzavřený port vygeneruje paket ICMP *Destination unreachable (Port unreachable)*

![[ps_wireshark_sU.png|700]]

### Příklad

```
sudo nmap -sU MACHINE_IP
```

![[ps_terminal_sU.png|650]]

- **port 111 je otevřený** (rpcbind)
- Nmap nedokáže určit, zda je **UDP port 68 otevřený nebo filtrovaný** (`open|filtered`)
- skenování trvalo **1085,05 s** – UDP skeny jsou pomalé

## Jemné doladění rozsahu a výkonu

### Specifikace portů

Místo výchozích **1000 portů** lze zadat vlastní:

- **seznam:** `-p22,80,443` – porty 22, 80 a 443
- **rozsah:** `-p1-1023` – všechny porty 1 až 1023 včetně; `-p20-25` – porty 20 až 25
- **všechny porty:** `-p-` – všech **65535** portů
- **100 nejběžnějších:** `-F`
- **top porty:** `--top-ports 10` – 10 nejběžnějších

### Časování skenování

- **`-T<0-5>`**: `-T0` je nejpomalejší (paranoidní), `-T5` nejrychlejší
- podle manuálové stránky Nmapu existuje **šest šablon** (viz [[časování skenování]]):
  - **paranoid (0)**, **sneaky (1)**, **polite (2)**, **normal (3)**, **aggressive (4)**, **insane (5)**
- vyhnutí se výstrahám **[[IDS]]**: `-T0` nebo `-T1`
  - `-T0` skenuje **jeden [[port]] po druhém** a mezi sondami čeká **5 minut**
- bez zadání časování používá Nmap **normální `-T3`**
- `-T5` je nejagresivnější z hlediska rychlosti, ale může ovlivnit **přesnost** výsledků (ztráta paketů)
- **`-T4`** se často používá při **CTF** a při učení na cvičných cílech, **`-T1`** během **skutečných střetnutí**, kde je důležitější utajení

### Rychlost paketů

- `--min-rate <number>` a `--max-rate <number>`
- příklad: `--max-rate 10` nebo `--max-rate=10` zajistí, že skener **neodešle víc než 10 paketů za sekundu**

### Paralelizace sond

- `--min-parallelism <numprobes>` a `--max-parallelism <numprobes>`
- Nmap zkoumá cíle (kteří hostitelé jsou aktivní, které porty otevřené); **paralelizace** udává, kolik sond může běžet **paralelně**
- příklad: `--min-parallelism=512` → Nmap udržuje **alespoň 512 sond** paralelně

## Shrnutí

Tři typy [[skenování portů]]:

| Typ skenování | Příkaz |
| :-- | :-- |
| [[TCP connect scan\|TCP Connect Scan]] | `nmap -sT MACHINE_IP` |
| [[SYN scan\|TCP SYN Scan]] | `sudo nmap -sS MACHINE_IP` |
| [[UDP scan\|UDP Scan]] | `sudo nmap -sU MACHINE_IP` |

Pomáhají zjišťovat **spuštěné služby TCP a UDP** na cílovém hostiteli.

| Volba | Účel |
| :-- | :-- |
| `-p-` | všechny porty |
| `-p1-1023` | porty 1 až 1023 |
| `-F` | 100 nejběžnějších portů |
| `-r` | skenovat porty v po sobě jdoucím pořadí |
| `-T<0-5>` | `-T0` nejpomalejší, `-T5` nejrychlejší |
| `--max-rate 50` | rychlost ≤ 50 paketů/s |
| `--min-rate 15` | rychlost ≥ 15 paketů/s |
| `--min-parallelism 100` | alespoň 100 sond paralelně |

## Související

[[nmap]] · [[skenování portů]] · [[stavy portů]] · [[hlavička TCP]] · [[TCP connect scan]] · [[SYN scan]] · [[UDP scan]] · [[časování skenování]] · [[SYN]] · [[ACK]] · [[RST]] · [[FIN]] · [[PSH]] · [[URG]] · [[3-way handshake]] · [[TCP]] · [[UDP]] · [[ICMP]] · [[port]] · [[firewall]] · [[IDS]] · [[Wireshark]] · [[Nmap příkazy]] · [[01_Nmap_Live_Host_Discovery|Live Host Discovery]] · [[03_Nmap_Advanced_Port_Scans|Advanced Port Scans]]
