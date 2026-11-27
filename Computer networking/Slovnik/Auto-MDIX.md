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

### Zapojení vodičů

- **přímý kabel** – na obou koncích stejné zapojení (T568B–T568B),
- **křížený kabel** – na jednom konci T568A, na druhém T568B,
- u 10/100 Mb/s se vysílá na pinech **1, 2** a přijímá na **3, 6**. Křížený kabel tyhle páry prohodí, aby vysílání jednoho šlo na příjem druhého.

| Spojení | Kabel bez Auto-MDIX |
| :-- | :-- |
| PC – switch, router – switch | přímý |
| switch – switch, PC – PC, router – router, PC – router | křížený |

Pravidlo: **stejný typ zařízení = křížený**, různý = přímý (PC a router se berou jako stejný typ).

### Příkazy na Cisco

```
S1(config-if)# mdix auto
S1# show controllers ethernet-controller fa0/1 phy | include MDIX
```

Auto-MDIX funguje jen se `speed auto` a `duplex auto`.

### Gigabit

1000BASE-T vysílá po všech čtyřech párech oběma směry najednou, takže Auto-MDIX je u gigabitu součástí standardu. Na gigabitových portech na typ kabelu skoro nezáleží.

**Souvisí:** [[UTP]], [[switch]], [[full-duplex]], [[NIC]]
