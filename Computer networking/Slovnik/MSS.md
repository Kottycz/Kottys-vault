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

### Příklad výpočtu

```
MTU Ethernetu          1500 B
− IP hlavička (IPv4)   − 20 B
− TCP hlavička         − 20 B
= MSS                  1460 B
```

U [[IPv6]] je IP hlavička 40 B, MSS je proto **1440 B**.

### MSS ve Wiresharku

MSS se posílá jako **volba (option) v SYN** a SYN-ACK při [[3-way handshake]]. Ve Wiresharku je v detailu SYN paketu: `Options: Maximum segment size: 1460 bytes`. Každá strana řekne, kolik umí přijmout, a použije se menší hodnota.

### Kdy je MSS menší

Přes [[VPN]] nebo PPPoE se k paketu přidávají další hlavičky, takže na data zbývá méně. Router pak MSS v SYN zmenší (`ip tcp adjust-mss 1360`), aby se pakety vešly a nemusely se fragmentovat.

**Souvisí:** [[MTU]], [[TCP]], [[3-way handshake]], [[goodput]], [[VPN]]
