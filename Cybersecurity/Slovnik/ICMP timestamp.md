---
aliases: [ICMP timestamp, ICMP časové razítko, -PP]
tags: [slovnik]
---

# ICMP timestamp

Typ [[ICMP]] zprávy, kterým se hostitel ptá na **čas** druhého; Nmap ho použije k zjištění, jestli je cíl online.

*Příklad: `nmap -PP -sn 10.10.68.220/24`.*

---

## Podrobně

| | Typ ICMP |
| :-- | :-- |
| požadavek na časové razítko | **13** |
| odpověď na časové razítko | **14** |

- přepínač Nmapu **`-PP`**
- používá se, když je **ICMP echo (ping) blokováno**
- v místnosti: 8 živých hostitelů za 10,93 s
- ve Wiresharku (filtr `icmp`) je vidět `Timestamp request` na každou IP v podsíti

**Souvisí:** [[ICMP]], [[ICMP address mask]], [[ping scan]], [[zjišťování živých hostitelů]]
