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

### Dvě varianty

| | Fast-forward | Fragment-free |
| :-- | :-- | :-- |
| kdy pošle rámec dál | hned po cílové MAC adrese (prvních 6 B za preambulí) | po prvních **64 bajtech** |
| latence | nejnižší | o trochu vyšší |
| kontrola | žádná | odfiltruje fragmenty po kolizi ([[runt|runty]]) |

Fragment-free využívá toho, že většina chyb z kolizí nastane v prvních 64 bajtech rámce.

### Srovnání se store-and-forward

| | Cut-through | [[store-and-forward]] |
| :-- | :-- | :-- |
| čeká na celý rámec | ne | ano |
| kontrola [[FCS]] | ne | ano |
| latence | nízká, stejná pro malé i velké rámce | roste s velikostí rámce |
| poškozené rámce | pošle dál | zahodí |

### Kde se používá

V datových centrech a u výpočetních clusterů, kde rozhodují mikrosekundy. Některé switche umí **adaptivní režim**: jedou cut-through, a když přibude chybných rámců, přepnou se na store-and-forward.

**Souvisí:** [[store-and-forward]], [[switch]], [[latency]]
