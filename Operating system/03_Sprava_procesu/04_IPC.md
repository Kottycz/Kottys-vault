---
aliases: [Interprocess Communication, IPC, Meziprocesová komunikace]
---

# IPC – meziprocesová komunikace

**[[proces|Procesy]]** jsou buď **nezávislé** (nesdílí data), nebo **spolupracující** (ovlivňují se a sdílí data). Spolupracující potřebují na výměnu dat **IPC (Interprocess Communication)**.

![[cd59faeda78bbe801c104cde8df72454310b8e881b4434174a10af9523fe8ec4.png]]

## Proč procesy spolupracují

- **sdílení informací** – víc uživatelů pracuje se stejnými daty
- **zrychlení výpočtu** – podúlohy běží paralelně (jen na víc jádrech)
- **modularita** – systém rozdělený na procesy/vlákna
- **pohodlí** – jeden uživatel dělá víc věcí najednou

**Chrome Multiprocess Architecture**

![[3d22816d7d44273a2dd1686a93f5903be1bb7e53f776f7a5360a62e3dad609f9.PNG]]

## Dva základní modely IPC

| Model | Princip | + | − |
| :-- | :-- | :-- | :-- |
| **Sdílená paměť** | společná oblast paměti, procesy do ní čtou a zapisují | rychlá – systémové volání jen při vytvoření | problémy s koherencí cache na víc jádrech |
| **Message passing** | procesy si posílají zprávy | bez konfliktů, snadné v distribuovaném systému, na víc jádrech dnes výkonnější | pomalejší – každá zpráva přes jádro |

## Sdílená paměť

- procesy souhlasí se zrušením běžné ochrany paměti a připojí si **sdílenou oblast** do svého adresového prostoru
- formát a umístění dat určují **procesy samy**, ne OS – a samy hlídají, aby nezapisovaly současně na stejné místo

### Producer–consumer problém

**Producer** data vyrábí, **consumer** je spotřebovává (např. kompilátor → assembler). Potřebují **buffer**:

- **neomezený** – producer může vyrábět vždy, consumer případně čeká na data
- **omezený** – consumer čeká, když je prázdný; producer čeká, když je plný

## Message-passing systémy

- komunikace a synchronizace **bez sdíleného adresového prostoru** – hlavně distribuované systémy
- operace **`send(message)`** a **`receive(message)`**
- komunikační spoj fyzicky: sdílená paměť, sběrnice, síť; logicky se řeší:
  1. **přímá × nepřímá** komunikace
  2. **synchronní × asynchronní**
  3. **automatické × explicitní** bufferování

### Přímá komunikace (Direct)

- procesy jmenují druhou stranu: `send(P, message)`, `receive(Q, message)`
- spoj vzniká automaticky, mezi dvojicí je právě jeden, obvykle obousměrný

### Nepřímá komunikace (Indirect)

- přes **poštovní schránky (mailbox, port)** s ID: `send(A, message)`, `receive(A, message)`
- spoj existuje jen mezi procesy se společnou schránkou; schránku může sdílet víc procesů, dvojice může mít víc schránek
- schránku vlastní **proces** (zanikne s ním) nebo **OS** (existuje samostatně)
- čte-li víc procesů, příjemce vybere systém (max. 1 najednou, round-robin, náhodně…)

### Synchronizace

| Typ | Chování |
| :-- | :-- |
| **Blocking send** | odesílatel čeká, dokud zprávu někdo nepřevezme |
| **Nonblocking send** | odešle a pokračuje |
| **Blocking receive** | příjemce čeká na zprávu |
| **Nonblocking receive** | vrátí zprávu nebo null |

- obě blokující = **rendezvous** → producer–consumer se řeší triviálně

### Bufferování front zpráv

- **nulová kapacita** – odesílatel vždy čeká na příjemce
- **omezená** (n zpráv) – čeká, jen když je fronta plná
- **neomezená** – nikdy nečeká

## Client–server komunikace

### Socket

- **koncový bod komunikace** = IP adresa + [[port]]
- server poslouchá na známém portu (Telnet 23, FTP 21, HTTP 80; pod 1024 = well-known), klient dostane náhodný port nad 1024
- spojení = unikátní dvojice socketů

![[3bc7980a3e77e12a449bdc09185ce81cb232c69b622f6c9a4a3c78bd1cd17091.png]]

### Remote Procedure Call (RPC)

- volání procedury přes síť
- **strukturovaná zpráva** pro RPC démona na portu vzdáleného systému: ID funkce + parametry; výsledek přijde zpět zprávou

![[e0d27e89de4e6d9405057d3f24466becc2087626740885eccca9e932d00bb263.png]]

### Roury (Pipes)

Jeden z prvních IPC mechanismů UNIXu – spojka mezi dvěma procesy. Otázky: jedno- nebo obousměrná? half/full duplex? nutný vztah rodič–potomek? přes síť?

#### Obyčejné roury (Ordinary Pipes)

- zápis na jednom konci, čtení na druhém, **jednosměrné** (obousměrně = dvě roury)
- jen mezi **rodičem a potomkem**, existují jen během komunikace
- Windows: „anonymní roury“

![[448c2bdc94dd713f5d4ef0fb0176e13ab9ad0bfd2f62d27279e4f5462bb06a54.png]]

#### Pojmenované roury (Named Pipes) – FIFO

- **obousměrné**, bez vztahu rodič–potomek, víc procesů, existují i po skončení procesů

| | UNIX (FIFO) | Windows |
| :-- | :-- | :-- |
| vytvoření | `mkfifo()` | `CreateNamedPipe()` |
| duplex | half-duplex | full-duplex |
| umístění | jen stejný stroj | i mezi stroji |
| data | bajtová | bajtová i zprávová |

**Souvisí:** [[proces]], [[port]], [[socket]], [[systémové volání]], [[proces synchronizace]]
