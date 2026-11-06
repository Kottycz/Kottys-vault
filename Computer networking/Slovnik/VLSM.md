---
aliases: [Variable Length Subnet Mask, subnetting]
tags: [slovnik]
---

# VLSM

**Variable Length Subnet Mask** – dělení sítě na podsítě **různých velikostí** podle skutečné potřeby, místo aby všechny byly stejně velké.

---

## Podrobně

### Proč

Kdyby se síť dělila jen na stejně velké kusy, plýtvalo by se: spoj mezi dvěma routery potřebuje 2 adresy, ale dostal by jich stejně jako oddělení se 100 počítači.

### Postup

1. Seřaď požadavky **od největšího k nejmenšímu**
2. Největší podsíti přiděl blok jako první
3. Z zbytku adres pokračuj další podsítí
4. Opakuj až k nejmenší

### Příklad

Máš `192.168.1.0/24` a potřebuješ:

| Podsíť | Hostů | Prefix | Rozsah |
| :-- | :-- | :-- | :-- |
| Výroba | 100 | **/25** (126) | 192.168.1.0 – .127 |
| Kanceláře | 50 | **/26** (62) | 192.168.1.128 – .191 |
| Servery | 20 | **/27** (30) | 192.168.1.192 – .223 |
| Spoj router–router | 2 | **/30** (2) | 192.168.1.224 – .227 |

Zbytek (.228–.255) zůstává volný pro budoucí použití.

### Jak zvolit prefix

Potřebuješ nejmenší blok, který se vejde:

```
Potřebuji 50 hostů
/26 → 2^6 − 2 = 62  ✓ stačí
/27 → 2^5 − 2 = 30  ✗ málo
```

Vždy pamatuj na −2 (adresa sítě + [[broadcast]]).

### Podmínka

Aby VLSM fungovalo, musí směrovací protokol posílat spolu s adresou i [[maska podsítě|masku]] – tzv. **classless** protokoly ([[OSPF]], EIGRP, RIPv2). Staré classful protokoly (RIPv1) to neumí.

**Souvisí:** [[maska podsítě]], [[délka prefixu]], [[IPv4]], [[broadcast]], [[OSPF]]
