---
aliases: [Automatic Medium-Dependent Interface Crossover, MDIX]
tags: [slovnik]
---

# Auto-MDIX

**Automatic Medium-Dependent Interface Crossover** – funkce, díky které si port sám pozná, jestli potřebuje přímý nebo křížený kabel, a vnitřně si vodiče prohodí.

---

## Podrobně

### Co řešilo křížení dřív

Ethernet používá jeden pár na vysílání (TX) a jiný na příjem (RX). Aby spojení fungovalo, musí TX jednoho zařízení dojít na RX druhého:

| Spojení | Dřív bylo potřeba |
| :-- | :-- |
| PC ↔ [[switch]] | **přímý** kabel |
| PC ↔ PC | **křížený** kabel |
| switch ↔ switch | **křížený** kabel |
| [[router]] ↔ PC | **křížený** kabel |

Mít v tašce oba typy kabelů bylo otravné a záměna znamenala, že linka prostě nenaběhla.

### Jak Auto-MDIX pomáhá

Port při připojení pozná, jaký typ kabelu je zapojený, a **elektronicky si TX/RX prohodí**, pokud je to potřeba. Funguje tedy jakýkoliv kabel.

### Podmínky

- Musí to podporovat **aspoň jedna** strana spojení
- Obvykle vyžaduje zapnutou **autonegotiation** (automatickou domluvu rychlosti a duplexu)
- U Cisco se zapíná příkazem `mdix auto` na rozhraní

### Dnešní stav

Prakticky všechna moderní zařízení (gigabitová a novější) mají Auto-MDIX **standardně zapnutý**, takže se rozdíl mezi přímým a kříženým kabelem v praxi přestal řešit. Znát ho je ale potřeba do testu a při práci se starším hardwarem.

**Souvisí:** [[UTP]], [[switch]], [[full-duplex]], [[NIC]]
