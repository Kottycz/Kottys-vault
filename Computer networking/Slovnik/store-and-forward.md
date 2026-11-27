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

### Proč je nutné při různých rychlostech

Když rámec přijde po linkě 1 Gb/s a má odejít linkou 100 Mb/s, switch ho nemůže posílat průběžně, protože by výstup nestíhal. Musí ho celý uložit do **bufferu** a odeslat pomaleji. To je store-and-forward.

### Latence podle velikosti rámce

Switch musí počkat, než dorazí celý rámec, takže zpoždění roste s velikostí:

| Rámec | Doba příjmu na 1 Gb/s |
| :-- | :-- |
| 64 B | ~0,5 µs |
| 1518 B | ~12 µs |

Pro běžnou kancelářskou síť je to zanedbatelné. Proto je store-and-forward výchozí metoda Cisco switchů.

### Buffering

| Typ | Popis |
| :-- | :-- |
| port-based | každý port má vlastní frontu, rámec může čekat kvůli jinému rámci před ním |
| shared memory | společná paměť pro všechny porty, pružnější, používají ji moderní switche |

**Souvisí:** [[cut-through]], [[switch]], [[FCS]], [[CRC]]
