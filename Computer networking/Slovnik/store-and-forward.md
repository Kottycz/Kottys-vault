---
aliases: [store-and-forward, ulož a předej]
tags: [slovnik]
---

# store-and-forward

**Store-and-forward** – metoda přepínání, kdy [[switch]] přijme **celý rámec**, zkontroluje ho a teprve pak ho pošle dál.

*Příklad: přijde poškozený rámec → switch zjistí chybu v FCS a rámec zahodí.*

---

## Podrobně

- uloží celý rámec do bufferu
- zkontroluje **CRC** (pole [[FCS]]) a délku rámce
- vadné rámce **zahodí** → neposílá chyby dál
- vyšší latence než [[cut-through]]
- nutné pro **QoS** a při různých rychlostech portů
- switch, který běží v cut-through, se při překročení chybovosti přepne na **store-and-forward**

| | Store-and-forward | Cut-through |
| :-- | :-- | :-- |
| kdy pošle rámec | po přijetí celého rámce | hned po cílové MAC adrese |
| kontrola chyb | ano (CRC) | ne |
| latence | vyšší | nízká |

**Souvisí:** [[cut-through]], [[switch]], [[FCS]], [[CRC]]
