---
aliases: [Maximum Segment Size]
tags: [slovnik]
---

# MSS

**Maximum Segment Size** – největší množství **užitečných dat** v jednom [[TCP]] segmentu (bez hlaviček). U Ethernetu obvykle **1460 bajtů**.

---

## Podrobně

### Jak se odvodí z MTU

Od [[MTU]] (1500 B) se odečtou hlavičky:

| Položka | Velikost |
| :-- | :-- |
| MTU | 1500 B |
| − IP hlavička | −20 B |
| − TCP hlavička | −20 B |
| **= MSS** | **1460 B** |

U [[IPv6]] je IP hlavička 40 B, takže MSS = 1440 B.

### Kdy se domlouvá

Obě strany si MSS řeknou při [[3-way handshake]] (v SYN paketu). Použije se **menší** z obou hodnot, aby to zvládly obě strany i linka mezi nimi.

### MSS vs. MTU

| | Co měří | Zahrnuje |
| :-- | :-- | :-- |
| **[[MTU]]** | největší paket na lince | IP hlavičku + obsah |
| **MSS** | největší data v segmentu | jen užitečná data |

MTU je vlastnost **linky** (vrstva 3), MSS je vlastnost **spojení** (vrstva 4).

### K čemu je to dobré

Když se MSS nastaví správně, TCP nikdy nevytvoří segment, který by se musel fragmentovat – přenos je efektivnější a spolehlivější.

### MSS clamping

Přes [[VPN]] nebo PPPoE je MTU menší, což někdy dělá problémy (stránky se nenačtou celé). [[router|Routery]] proto umí **MSS clamping** – přepíší MSS v procházejících SYN paketech na nižší hodnotu, aby segmenty prošly.

**Souvisí:** [[MTU]], [[TCP]], [[3-way handshake]], [[goodput]], [[VPN]]
