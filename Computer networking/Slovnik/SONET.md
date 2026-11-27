---
aliases: [Synchronous Optical Networking, SDH, Synchronous Digital Hierarchy]
tags: [slovnik]
---

# SONET

**Synchronous Optical Networking** – standard pro přenos dat po [[optické vlákno|optice]] na dlouhé vzdálenosti. Evropská obdoba se jmenuje **SDH**.

---

## Podrobně

### K čemu slouží

Páteřní technologie poskytovatelů ([[WAN]]) – propojuje města a země. Pracuje na fyzické a spojové vrstvě, přenáší po optice data z vyšších protokolů (např. IP).

### SONET vs. SDH

| | SONET | SDH |
| :-- | :-- | :-- |
| Rozšíření | Severní Amerika | Evropa, zbytek světa |
| Základní rychlost | 51,84 Mb/s (OC-1) | 155 Mb/s (STM-1) |

Jsou vzájemně kompatibilní, jde v podstatě o dvě verze téhož.

### Vlastnosti

- **Synchronní** – celá síť běží na přesných hodinách, data mají pevné časové sloty
- **Vysoká spolehlivost** – kruhová [[topologie]] s automatickým přepnutím na záložní trasu při přerušení vlákna (do 50 ms)
- **Pevné rychlosti** – OC-3 (155 Mb/s), OC-12, OC-48, OC-192 (10 Gb/s)

### Dnešní stav

Postupně se nahrazuje modernějšími technologiemi (**OTN**, Carrier Ethernet, DWDM), které lépe vyhovují datovému provozu. SONET/SDH byl navržen hlavně pro telefonní okruhy s pevnou kapacitou, což je pro dnešní proměnlivý datový provoz neefektivní.

### Rychlosti

| SONET | SDH | Rychlost |
| :-- | :-- | :-- |
| OC-3 | STM-1 | 155 Mb/s |
| OC-12 | STM-4 | 622 Mb/s |
| OC-48 | STM-16 | 2,5 Gb/s |
| OC-192 | STM-64 | 10 Gb/s |

SONET se používá v Severní Americe, v Evropě (i v Česku) **SDH**.

### Kruhová topologie

SONET/SDH sítě se staví jako **dvojitý kruh**. Když se vlákno přeruší, provoz se otočí druhým směrem do **50 ms** – hovory to ani nepoznají.

### DWDM

Na jednom vlákně dnes běží mnoho přenosů současně na různých **vlnových délkách** (barvách) světla. Technologie **DWDM** tak zmnohonásobí kapacitu existujících vláken.

**Souvisí:** [[optické vlákno]], [[WAN]], [[ISP]], [[topologie]]
