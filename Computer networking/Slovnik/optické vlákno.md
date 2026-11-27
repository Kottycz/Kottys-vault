---
aliases: [optika, SMF, MMF, jednovidové vlákno, multimódové vlákno, FTTH]
tags: [slovnik]
---

# optické vlákno

**Tenké skleněné vlákno přenášející data pomocí světla.** Má minimální útlum, obrovskou kapacitu a je **úplně imunní** vůči [[EMI|rušení]].

---

## Podrobně

### Princip

Vlákno funguje jako světlovod – světlo se uvnitř odráží od stěn a putuje i na velké vzdálenosti bez výrazné ztráty. Vlákno je jen o málo silnější než lidský vlas.

### Dva typy

| Typ | Jádro | Zdroj světla | Dosah | Použití |
| :-- | :-- | :-- | :-- | :-- |
| **SMF** (jednovidové) | úzké (~9 µm) | laser | desítky až stovky km | páteřní a dálkové spoje |
| **MMF** (multimódové) | širší (~50 µm) | LED / VCSEL | stovky metrů | uvnitř budov, datacentra |

U MMF se světlo odráží pod víc úhly (víc "vidů"), což omezuje dosah. SMF vede světlo prakticky přímo – proto zvládne mnohem delší trasy.

### Výhody proti metalickému kabelu

- **Obrovská kapacita** a [[throughput]]
- **Velký dosah** – desítky kilometrů bez zesilovače (u [[UTP]] jen 100 m)
- **Imunita vůči [[EMI]] a RFI** – ideální do průmyslu
- **Nevyzařuje signál** – nejde snadno odposlechnout

### Nevýhody

- Dražší (hlavně koncová zařízení a svařování vláken)
- Křehčí, nesnese ostré ohyby
- Instalace vyžaduje speciální nástroje a školení

### Kde se používá

- **Páteřní sítě** poskytovatelů a propojení měst
- **FTTH** (Fiber To The Home) – optika až do domácnosti
- **Datacentra** – propojení switchů a serverů
- **Podmořské kabely** mezi kontinenty

### Konektory

| Konektor | Popis |
| :-- | :-- |
| **SC** | čtvercový, zacvakává se, starší standard |
| **LC** | malý, dnes nejběžnější (do SFP modulů) |
| **ST** | kulatý s bajonetem, starší |

Optika obvykle používá **dvě vlákna** – jedno pro vysílání, druhé pro příjem.

### Single-mode vs. multimode

| | Single-mode (SMF) | Multimode (MMF) |
| :-- | :-- | :-- |
| jádro | velmi tenké (~9 µm) | silnější (50–62,5 µm) |
| zdroj světla | laser | LED nebo levný laser |
| dosah | desítky km | stovky metrů |
| cena | vyšší | nižší |
| barva pláště (typicky) | žlutá | oranžová nebo tyrkysová |

### Bezpečnost práce

Nedívat se do konce vlákna nebo do portu – laserové světlo je neviditelné a může poškodit zrak. Úlomky skla z vláken jsou ostré a špatně se hledají.

**Souvisí:** [[UTP]], [[EMI]], [[throughput]], [[WAN]], [[ISP]]
