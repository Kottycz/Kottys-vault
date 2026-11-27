---
aliases: [Digital Subscriber Line, ADSL, SDSL, VDSL]
tags: [slovnik]
---

# DSL

**Digital Subscriber Line** – digitální účastnická linka. Internet přenášený po **telefonní lince** na frekvencích, které telefonie nevyužívá.

---

## Podrobně

### Princip

Telefonní hovor potřebuje jen nízké frekvence. DSL použije zbytek pásma pro data – proto může po jednom kabelu jet telefon i internet zároveň. Oddělí je **splitter** (filtr) u zákazníka.

### Varianty

| Zkratka | Název | Vlastnost |
| :-- | :-- | :-- |
| **ADSL** | Asymmetric DSL | stahování rychlejší než odesílání – pro domácnosti |
| **SDSL** | Symmetric DSL | stejná rychlost oběma směry – pro firmy |
| **VDSL** | Very high speed DSL | vyšší rychlosti, ale kratší dosah |

### Proč je asymetrické

Běžný uživatel víc stahuje (video, web) než odesílá, takže se kapacita rozdělí nerovnoměrně. Firma naopak potřebuje i odesílat (server, zálohy, videokonference) – proto SDSL.

### Omezení

- **Rychlost klesá se vzdáleností** od ústředny – pár kilometrů a je po výkonu
- Závisí na kvalitě staré telefonní kabeláže
- Oproti optice a kabelu výrazně pomalejší

### Srovnání s ostatními technologiemi

| Technologie | Médium | Rychlost | Symetrie |
| :-- | :-- | :-- | :-- |
| **DSL** | telefonní linka | nižší | obvykle ne |
| Kabel | koaxiál (TV rozvody) | vysoká | ne |
| **[[optické vlákno\|Optika]]** | vlákno | nejvyšší | ano |
| Mobilní | 4G/5G | proměnlivá | ne |
| Satelit | rádio | nízká, velká [[latency\|latence]] | ne |

DSL se dnes postupně nahrazuje optikou, ale v místech bez optické infrastruktury se pořád používá.

### Části DSL přípojky

- **DSL modem** u zákazníka – převádí data na signál pro telefonní linku,
- **splitter / mikrofiltr** – oddělí telefonní hovory od dat, aby se navzájem nerušily,
- **DSLAM** u poskytovatele – sbírá linky od mnoha zákazníků a připojuje je do sítě [[ISP]].

### Vzdálenost

Signál po měděné lince slábne ([[útlum]]). Čím dál je zákazník od ústředny, tím nižší rychlost. ADSL funguje do zhruba 5 km, VDSL2 dává vysoké rychlosti jen na krátké vzdálenosti (stovky metrů), proto se kombinuje s optikou dovedenou až do ulice.

**Souvisí:** [[ISP]], [[WAN]], [[optické vlákno]], [[latency]], [[šířka pásma]]
