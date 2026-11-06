---
aliases: [cut-through, fragment-free, fast-forward]
tags: [slovnik]
---

# cut-through

**Cut-through** – metoda přepínání, kdy [[switch]] začne posílat rámec dál, **jakmile přečte cílovou MAC adresu**, bez čekání na celý rámec.

*Příklad: switch v datacentru, kde záleží na co nejnižší latenci.*

---

## Podrobně

- velmi **nízká latence**
- nekontroluje chyby → může přeposlat i poškozený rámec nebo **runt** (příliš krátký rámec)

| Varianta | Kdy pošle rámec |
| :-- | :-- |
| **fast-forward** | hned po cílové MAC adrese (nejnižší latence) |
| **fragment-free** | po prvních 64 bajtech → odfiltruje většinu kolizních fragmentů |

- při překročení chybovosti se switch přepne na [[store-and-forward]]

**Souvisí:** [[store-and-forward]], [[switch]], [[latency]]
