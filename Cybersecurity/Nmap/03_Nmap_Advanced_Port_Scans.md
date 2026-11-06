# Nmap – Advanced Port Scans

TryHackMe: **MTA-Nmap Advanced Port Scans** (třetí ze čtyř místností o Nmapu, součást modulu MTA – Základní dovednosti). Pokročilé typy [[skenování portů]], obcházení [[firewall|firewallů]] a [[IDS]], falšování adres a získání více podrobností.

## Úvod

- v prvních dvou místnostech: **zjišťování živých hostitelů** ([[01_Nmap_Live_Host_Discovery|Live Host Discovery]]) a **základní [[skenování portů]]** ([[02_Nmap_Basic_Port_Scans|Basic Port Scans]])
- v Basic Port Scans: [[hlavička TCP|TCP příznaky]] a **třícestný handshake** ([[3-way handshake]])
  - k zahájení připojení vyžaduje [[TCP]], aby měl první paket nastaven příznak **[[SYN]]**
  - podle odpovědi se pozná, zda je [[port]] [[TCP]] otevřený
- bezpečnostní výzkumníci a hackeři se zamysleli nad příznaky TCP a začali **experimentovat**: co se stane, když pošleme TCP paket, který **není součástí žádného probíhajícího spojení**, s jedním nebo více nastavenými příznaky
- příklad: příznak **[[ACK]]** se nastavuje, když chceme potvrdit přijatá data; **skenování [[ACK]]** je jako někdo, kdo za vámi z ničeho nic přijde a řekne „Ano, slyším tě, prosím pokračuj“, když jsi nic neřekl

![[ps_tcp_hlavicka.png|600]]

### Co se probírá

Typy skenování portů:

- [[Null scan]]
- [[FIN scan]]
- [[Xmas scan]]
- [[Maimon scan]]
- [[ACK scan]]
- [[Window scan]]
- [[custom scan|Custom scan]]

Dále:

- [[IP spoofing|Spoofing IP]]
- [[MAC spoofing|Spoofing MAC]]
- [[decoy scan|Decoy scan]]
- [[fragmentace paketů|Fragmentované pakety]]
- [[idle scan|Idle/Zombie scan]]

Také **techniky obejití firewallů a systémů [[IDS]]** a možnosti, jak z Nmapu získat **větší podrobnosti**.

## TCP Null, FIN a Xmas Scan

Tři typy skenování, které využívají **neočekávané kombinace příznaků**:

1. **[[Null scan|Null Scan]]**
2. **[[FIN scan|FIN Scan]]**
3. **[[Xmas scan|Xmas Scan]]**

Společné: **uzavřený** [[port]] odpoví **[[RST]]**, u otevřeného portu **odpověď nepřijde**.

### 1. Null Scan (`-sN`)

- **nenastaví žádný příznak** – všech šest příznakových bitů v hlavičce [[TCP]] je **0**
- spuštění: **`-sN`**
- paket TCP bez příznaků nespustí **žádnou odpověď**, když dosáhne otevřeného portu
- Nmap z nedostatku odpovědi pozná jen to, že je port **buď otevřený, nebo blokovaný firewallem**

![[adv_diagram_sN_otevreny.png|600]]

- cílový server odpoví **RST**, pokud je port **uzavřen**
- **nedostatek odpovědi RST** tedy značí porty, které nejsou zavřené: **otevřené nebo filtrované**

![[adv_diagram_sN_uzavreny.png|600]]

Příklad (`sudo nmap -sN MACHINE_IP`):

![[adv_terminal_sN.png|650]]

- úspěšně identifikoval **šest otevřených portů** (stav `open|filtered`)
- protože Null scan spoléhá na **absenci odpovědi**, nemůže s jistotou říct, že jsou porty otevřené; mohou nereagovat kvůli **pravidlu firewallu**
- mnoho možností Nmapu vyžaduje **oprávnění root** → je třeba použít **`sudo`**

### 2. FIN Scan (`-sF`)

- pošle paket TCP s nastaveným příznakem **[[FIN]]**
- spuštění: **`-sF`**
- podobně **nebude odeslána žádná odpověď**, pokud je port otevřený; Nmap si nemůže být jistý, zda je otevřený, nebo zda [[firewall]] blokuje provoz

![[adv_diagram_sF_otevreny.png|600]]

- cílový systém by měl odpovědět **RST**, pokud je port **uzavřen**
- známe tedy zavřené porty a můžeme odvodit porty **otevřené nebo filtrované**
- **některé firewally „potichu“ zastaví provoz bez odeslání RST**

![[adv_diagram_sF_uzavreny.png|600]]

Příklad (`sudo nmap -sF MACHINE_IP`) – výsledek velmi podobný Null scanu:

![[adv_terminal_sF.png|650]]

### 3. Xmas Scan (`-sX`)

- název podle rozsvícení **vánočního stromku**
- nastavuje **současně příznaky [[FIN]], [[PSH]] a [[URG]]**
- spuštění: **`-sX`**
- stejně jako u Null a FIN scanu: přijat **RST** = port je **uzavřen**; jinak bude hlášen jako **`open|filtered`**

![[adv_diagram_sX_otevreny.png|600]]

![[adv_diagram_sX_uzavreny.png|600]]

Příklad (`sudo nmap -sX MACHINE_IP`) – výsledky velmi podobné Null a FIN scanu:

![[adv_terminal_sX.png|650]]

### Kdy jsou tyto tři skeny účinné

- jeden ze scénářů: skenování cíle za **bezstavovou (nestavovou) bránou firewall**
- **bezstavový firewall** kontroluje, zda má příchozí paket nastaven příznak **[[SYN]]** (detekce pokusu o připojení)
- kombinace příznaků, která **neodpovídá paketu SYN**, umožňuje **oklamat firewall** a dostat se do systému za ním
- **[[stavový firewall]]** takto vytvořené pakety zablokuje → druh skenování je pak **zbytečný** (viz [[stavový firewall]])

## TCP Maimon Scan (`-sM`)

- **Uriel Maimon** poprvé popsal tento sken v roce **1996**
- nastaveny jsou bity **[[FIN]] a [[ACK]]**
- cíl by měl odeslat paket **[[RST]]** jako odpověď
- některé systémy odvozené od **BSD** ale paket **zahodí**, pokud se jedná o otevřený [[port]] → odhalují otevřené porty
- na většině moderních cílů **nefunguje**, ale je zařazen, abychom lépe porozuměli mechanismům [[skenování portů]] a přístupu hackerů
- spuštění: **`-sM`**

![[adv_diagram_sM.png|600]]

- většina cílových systémů odpovídá **RST bez ohledu na to, zda je port [[TCP]] otevřený** → otevřené porty tak nelze objevit

Příklad (`sudo nmap -sM 10.10.252.27`) – **všech 1000 portů vyhodnoceno jako zavřené**, žádný otevřený port nenalezen:

![[adv_terminal_sM.png|650]]

- není to první sken, který bys zvolil k objevení systému, ale je důležité o něm vědět

## TCP ACK, Window a Custom Scan

### TCP ACK Scan (`-sA`)

- odešle paket [[TCP]] s nastaveným příznakem **[[ACK]]**
- spuštění: **`-sA`**
- cíl odpoví **[[RST]] bez ohledu na stav portu**
  - důvod: TCP paket s příznakem [[ACK]] by měl být odeslán jen jako **odpověď** na přijatý paket, aby potvrdil přijetí dat
- v jednoduchém nastavení nám sken **neřekne, zda je cílový [[port]] otevřený**

![[adv_diagram_sA.png|600]]

Příklad **před** instalací firewallu – podle očekávání se nedozvíme, které porty jsou otevřené (všech 1000 je `unfiltered`):

![[adv_terminal_sA_bez_firewallu.png|650]]

- užitečný, pokud je před cílem **[[firewall]]**: podle toho, které ACK pakety vedly k odpovědím, se dozvíš, **které porty nebyly firewallem blokovány**
- hodí se spíš pro zjištění **sady pravidel a konfigurace** firewallu

Po nastavení cílového VM s **firewallem** – tři porty firewall **neblokuje**, ostatní blokuje:

![[adv_terminal_sA_firewall.png|650]]

### TCP Window Scan (`-sW`)

- téměř stejný jako **skenování ACK**, ale zkoumá **pole TCP Window** vrácených paketů **RST**
- na konkrétních systémech může odhalit, že je port **otevřený**
- spuštění: **`-sW`**
- očekáváme paket **RST** jako odpověď na „nezvané“ pakety ACK, bez ohledu na to, zda je port otevřený nebo zavřený

![[adv_diagram_sW.png|600]]

Proti Linuxu **bez firewallu** neposkytne mnoho informací (žádné další oproti skenu ACK):

![[adv_terminal_sW_bez_firewallu.png|650]]

Za **firewallem** dává uspokojivější výsledky – **tři porty detekovány jako uzavřené** ([[ACK scan]] je označil jako nefiltrované). Víme, že nejsou zavřené, takže **reagovaly odlišně**, což znamená, že je firewall neblokuje:

![[adv_terminal_sW_firewall.png|650]]

### Custom Scan (`--scanflags`)

- chceš-li experimentovat s **novou kombinací příznaků TCP** nad rámec vestavěných typů skenování, použij **`--scanflags`**
- příklad: nastavit **[[SYN]], RST a [[FIN]]** současně → `--scanflags RSTSYNFIN`
- při vlastním skenování musíš vědět, **jak se budou různé porty chovat**, abys správně interpretoval výsledky

![[adv_diagram_scanflags.png|600]]

- `--scanflags URGACKPSHRSTSYNFIN` nastaví **všechny** příznaky

### Důležité

- **TCP ACK scan** a **TCP [[Window scan]]** velmi účinně pomáhají **zmapovat pravidla firewallu**
- to, že firewall neblokuje konkrétní port, **nemusí znamenat**, že služba na tomto portu naslouchá (pravidla firewallu mohou být zastaralá)
- proto ACK a Window scan **odhalují pravidla firewallu, nikoli služby**

## Spoofing a Decoys

- v některých nastaveních sítě lze cíl skenovat pomocí **falešné IP adresy** a dokonce i **falešné MAC adresy**
- takové skenování je výhodné **jen když můžeš zaručit zachycení odezvy**
- pokud se skenuje z náhodné sítě podvrženou IP adresou, je pravděpodobné, že **odpověď nebude směrována na tebe** a výsledky mohou být nespolehlivé

### Spoofing IP (`-S`)

- příkaz: `nmap -S SPOOFED_IP MACHINE_IP`
- Nmap vytvoří všechny pakety s poskytnutou **zdrojovou IP adresou** (SPOOFED_IP)
- cílový počítač odpoví **na podvrženou adresu**
- aby sken fungoval, musí útočník **sledovat síťový provoz** a analyzovat odpovědi

![[adv_diagram_spoofing_ip.png|600]]

Stručně, tři kroky:

1. útočník odešle paket s **podvrženou zdrojovou IP adresou** do cílového počítače
2. cílový počítač odpoví na podvrženou IP adresu jako na **cíl**
3. útočník **zachytává odpovědi**, aby zjistil otevřené porty

V praxi:

- obecně se specifikuje **síťové rozhraní** pomocí **`-e`** a explicitně se zakáže **[[ping scan]]** pomocí **`-Pn`**
- místo `nmap -S SPOOFED_IP MACHINE_IP` tedy: `nmap -e NET_INTERFACE -Pn -S SPOOFED_IP MACHINE_IP`
- bez toho Nmap neví, které rozhraní použít, a nečeká odpověď na ping
- sken bude **k ničemu**, pokud systém útočníka nemůže sledovat odpověď sítě

### Spoofing MAC (`--spoof-mac`)

- jsi-li ve **stejné podsíti** jako cíl, můžeš podvrhnout i **[[MAC adresa|MAC adresu]]**
- zdrojová MAC: **`--spoof-mac SPOOFED_MAC`**
- možné **jen** pokud jsou útočník a cíl ve stejné síti **Ethernet (802.3)** nebo stejné **WiFi (802.11)**
- spoofing funguje jen v minimálním počtu případů, kdy jsou splněny určité podmínky

### Decoy Scan (`-D`)

- útočník se může uchýlit k použití **návnad**, aby bylo obtížnější jej určit
- sken vypadá, že přichází z **mnoha IP adres**, takže se **útočníkova [[IP adresa]] mezi nimi ztratí**
- odpovědi chodí i na adresy návnad

![[adv_diagram_decoy.png|600]]

- spuštění: **`-D`** s konkrétními nebo náhodnými IP adresami
- `nmap -D 10.10.0.1,10.10.0.2,ME MACHINE_IP` → sken MACHINE_IP bude vypadat jako z 10.10.0.1 a 10.10.0.2; **`ME`** označuje, že tvoje IP se má objevit **ve třetím pořadí**
- `nmap -D 10.10.0.1,10.10.0.2,RND,RND,ME MACHINE_IP` → třetí a čtvrtá zdrojová IP se přiřadí **náhodně** (**`RND`**), pátý zdroj je IP útočníka

## Fragmentované pakety

### Firewall

- **[[firewall]]** je část softwaru nebo hardwaru, která umožňuje paketům **procházet nebo je blokuje**
- pracuje podle **pravidel**:
  - blokování veškerého provozu **s výjimkami** (co není zakázáno, je povoleno) *nebo*
  - povolení veškerého provozu **s výjimkami** (co není povoleno, je zakázáno)
- příklad: zablokovat veškerý provoz na server **kromě** provozu na webový server
- **tradiční firewall** kontroluje alespoň **hlavičku IP** a **hlavičku transportní vrstvy**
- **sofistikovanější** se pokusí prozkoumat i **data** přenášená transportní vrstvou

![[adv_firewall_obrazek.png|600]]

### IDS

- **[[IDS]]** (Intrusion Detection System) kontroluje síťové pakety na **vzorce chování** nebo **specifické podpisy obsahu**
- **vyvolá výstrahu**, kdykoli je splněno škodlivé pravidlo
- kromě hlaviček IP a transportní vrstvy kontroluje i **obsah dat** v transportní vrstvě
- jak snížit pravděpodobnost, že tradiční firewall/IDS zjistí aktivitu Nmapu? Podle typu firewallu/IDS může pomoci **rozdělení paketů na menší pakety**

### Fragmentace (`-f`)

- **`-f`** fragmentuje pakety: data IP se rozdělí na **8 bajtů nebo méně**
- další **`-f`** (`-f -f` nebo **`-ff`**) → data se rozdělí na **16bajtové** fragmenty místo 8
- výchozí hodnotu lze změnit pomocí **`--mtu`** (vždy násobek 8)
- k pochopení fragmentace je potřeba znát **[[hlavička IP|hlavičku IP]]**:
  - **zdrojová adresa** zabírá 32 bitů (4 bajty) na čtvrtém řádku, **cílová** další 4 bajty na pátém
  - data, která se fragmentují, jsou zvýrazněna červeně
  - pro opětovné sestavení na straně příjemce se používá **IP identifikace (ID)** a **ofset fragmentů** (druhý řádek)

![[adv_ip_hlavicka.png|600]]

Porovnání příkazů:

- `sudo nmap -sS -p80 10.20.30.144`
- `sudo nmap -sS -p80 -f 10.20.30.144`

Oba používají **tajné skenování [[TCP]] [[SYN]]** na portu 80; druhý navíc žádá o **fragmentaci IP paketů**.

Bez fragmentace:

- první dva řádky: **dotaz [[ARP]] a odpověď** (cíl je na stejném Ethernetu)
- další dva řádky: **TCP SYN [[ping]] a odpověď**
- pátý řádek je začátek [[skenování portů]]: Nmap odešle **TCP SYN na [[port]] 80**
- [[hlavička IP]] má **20 bajtů**, [[hlavička TCP]] **24 bajtů** (minimální velikost hlavičky TCP je 20 bajtů)

![[adv_wireshark_bez_fragmentace.png|700]]

S fragmentací (`-f`):

- 24 bajtů hlavičky TCP se rozdělí na **násobky 8**, poslední fragment obsahuje 8 bajtů nebo méně
- protože 24 je dělitelné 8 → **3 fragmenty IP**, každý má **20 bajtů hlavičky IP + 8 bajtů hlavičky TCP**
- tři fragmenty jsou mezi pátým a sedmým řádkem

![[adv_wireshark_fragmentace_f.png|700]]

- s **`-ff`** (nebo `-f -f`) je fragmentace po násobcích **16**: 24 bajtů TCP se rozdělí na **dva fragmenty** (16 a 8 bajtů)
- naopak pokud dáváš přednost **zvětšení velikosti paketů**, aby vypadaly neškodně: **`--data-length NUM`** (NUM = počet bajtů, které se připojí k paketům)

## Idle/Zombie Scan (`-sI`)

- spoofing zdrojové IP je skvělý přístup k **tajnému skenování**, ale funguje jen ve **specifických síťových nastaveních** (musíš být v pozici, kde můžeš sledovat provoz)
- proto ho lze **upgradovat** skenováním při nečinnosti
- **[[idle scan|Idle (zombie) scan]]** vyžaduje **nečinný systém** připojený k síti, se kterým můžeš komunikovat
- Nmap způsobí, že každá sonda **vypadá, jako by přicházela z nečinného (zombie) hostitele**, a pak zkontroluje, zda nečinný hostitel obdržel nějakou **odpověď** na podvrženou sondu
- toho se dosáhne kontrolou hodnoty **[[IP ID]]** v hlavičce IP
- příkaz: **`nmap -sI ZOMBIE_IP MACHINE_IP`** (ZOMBIE_IP = IP nečinného hostitele)

### Tři kroky

1. **spusť nečinného hostitele**, aby odpověděl → zaznamenej aktuální **[[IP ID]]** na nečinném hostiteli
2. **odešli paket [[SYN]]** na [[TCP]] [[port]] v cíli; paket je **podvržen**, aby vypadal, že pochází z IP adresy nečinného hostitele (zombie)
3. **znovu spusť nečinný počítač**, aby odpověděl → porovnej **nové IP ID** s dříve přijatým

Příklad: útočník zkoumá nečinný stroj, **multifunkční tiskárnu**. Odesláním **SYN/ACK** odpoví paketem **[[RST]]** obsahujícím jeho nově zvýšené IP ID.

![[adv_diagram_zombie_ip_id.png|500]]

Útočník pak odešle paket **SYN** na TCP port v cíli, ale jako zdroj použije **IP adresu zombie**. Vzniknou **tři scénáře**:

**1. Port je uzavřen** – cíl odpoví zombie paketem **RST**. Zombie nereaguje, proto se jeho **IP ID nezvyšuje**.

![[adv_diagram_zombie_uzavreny.png|500]]

**2. Port je otevřen** – cíl odpoví zombie **SYN/ACK**. Zombie na neočekávaný paket odpoví **RST**, čímž **zvýší své IP ID**.

![[adv_diagram_zombie_otevreny.png|500]]

**3. Cíl vůbec nereaguje** (kvůli pravidlům **firewallu**) – stejný výsledek jako u uzavřeného portu: nečinný hostitel **nezvýší IP ID**.

**Poslední krok:** útočník odešle další **SYN/ACK** zombie. Zombie odpoví **RST** a opět zvýší IP ID o jedna. Útočník porovná IP ID prvního a posledního RST:

| Rozdíl IP ID | Význam |
| :-- | :-- |
| **1** | port na cíli je **uzavřen nebo filtrován** |
| **2** | port na cíli je **otevřený** |

- sken se jmenuje **nečinný**, protože **výběr nečinného hostitele je nezbytný pro přesnost** – pokud „nečinný hostitel“ zaneprázdněn, všechna vrácená IP ID by byla k ničemu

## Získání dalších podrobností

### `--reason`

- chceš-li, aby Nmap poskytl **další podrobnosti o svém odůvodnění a závěrech**, přidej **`--reason`**

Bez `--reason` (`sudo nmap -sS 10.10.252.27`):

![[adv_terminal_sS.png|650]]

S `--reason` (`sudo nmap -sS --reason 10.10.252.27`):

![[adv_terminal_sS_reason.png|650]]

- příznak dává **explicitní důvod**, proč Nmap dospěl k závěru, že systém funguje nebo je [[port]] otevřený
- systém je považován za online, protože Nmap **„přijal arp-response“**
- port **[[SSH]]** je otevřený, protože Nmap obdržel zpět paket **„syn-ack“**

### Podrobnější výstup

- **`-v`** = podrobný výstup (verbose), **`-vv`** = ještě podrobnější

![[adv_terminal_sS_vv.png|650]]

- **`-d`** = ladění (debugging), **`-dd`** = ještě více podrobností; použití `-d` vytvoří výstup, který přesahuje jednu obrazovku

## Shrnutí

| Typ skenování | Příklad příkazu |
| :-- | :-- |
| [[Null scan\|TCP Null Scan]] | `sudo nmap -sN MACHINE_IP` |
| [[FIN scan\|TCP FIN Scan]] | `sudo nmap -sF MACHINE_IP` |
| [[Xmas scan\|TCP Xmas Scan]] | `sudo nmap -sX MACHINE_IP` |
| [[Maimon scan\|TCP Maimon Scan]] | `sudo nmap -sM MACHINE_IP` |
| [[ACK scan\|TCP ACK Scan]] | `sudo nmap -sA MACHINE_IP` |
| [[Window scan\|TCP Window Scan]] | `sudo nmap -sW MACHINE_IP` |
| [[custom scan\|Custom TCP Scan]] | `sudo nmap --scanflags URGACKPSHRSTSYNFIN MACHINE_IP` |
| [[IP spoofing\|Spoofed Source IP]] | `sudo nmap -S SPOOFED_IP MACHINE_IP` |
| [[MAC spoofing\|Spoofed MAC Address]] | `--spoof-mac SPOOFED_MAC` |
| [[decoy scan\|Decoy Scan]] | `nmap -D DECOY_IP,ME MACHINE_IP` |
| [[idle scan\|Idle (Zombie) Scan]] | `sudo nmap -sI ZOMBIE_IP MACHINE_IP` |
| [[fragmentace paketů\|Fragmentace IP dat na 8 bajtů]] | `-f` |
| [[fragmentace paketů\|Fragmentace IP dat na 16 bajtů]] | `-ff` |

| Volba | Účel |
| :-- | :-- |
| `--source-port PORT_NUM` | určit číslo zdrojového portu |
| `--data-length NUM` | připojit náhodná data do dané délky |
| `--reason` | vysvětlí, jak Nmap dospěl k závěru |
| `-v` | verbose (podrobně) |
| `-vv` | very verbose (velmi podrobně) |
| `-d` | ladění (debugging) |
| `-dd` | více podrobností pro ladění |

- tyto typy skenování spoléhají na **nastavení příznaků [[TCP]] neočekávaným způsobem**, aby porty vyvolaly odpověď
- **Null, [[FIN]] a Xmas** scan vyvolávají odezvu **uzavřených** portů
- **Maimon, [[ACK]] a Window** skeny vyvolávají odezvu **otevřených i zavřených** portů

## Související

[[nmap]] · [[skenování portů]] · [[stavy portů]] · [[Null scan]] · [[FIN scan]] · [[Xmas scan]] · [[Maimon scan]] · [[ACK scan]] · [[Window scan]] · [[custom scan]] · [[IP spoofing]] · [[MAC spoofing]] · [[decoy scan]] · [[fragmentace paketů]] · [[idle scan]] · [[IP ID]] · [[hlavička IP]] · [[hlavička TCP]] · [[stavový firewall]] · [[IDS]] · [[firewall]] · [[SYN]] · [[ACK]] · [[RST]] · [[FIN]] · [[PSH]] · [[URG]] · [[TCP]] · [[MAC adresa]] · [[Nmap příkazy]] · [[02_Nmap_Basic_Port_Scans|Basic Port Scans]] · [[04_Nmap_Post_Port_Scans|Post Port Scans]]
