---
aliases: [Enhanced Interior Gateway Routing Protocol]
tags: [slovnik]
---

# EIGRP

**Enhanced Interior Gateway Routing Protocol** – směrovací protokol od Cisca pro směrování uvnitř jedné sítě (AS). Kombinuje vlastnosti distance vector a link-state protokolů.

---

## Podrobně

### Vlastnosti

- **Původně proprietární** (jen Cisco), od roku 2013 částečně otevřený
- **Rychlá konvergence** – díky algoritmu **DUAL** drží záložní cesty připravené předem
- **Classless** – posílá [[maska podsítě|masku]], podporuje [[VLSM]]
- Podporuje [[IPv4]] i [[IPv6]]
- Používá [[multicast]] 224.0.0.10

### Metrika

Na rozdíl od [[OSPF]] (jen šířka pásma) počítá EIGRP metriku z víc parametrů:

| Parametr | Ve výchozím nastavení |
| :-- | :-- |
| Šířka pásma | **ano** |
| Zpoždění | **ano** |
| Zatížení | ne |
| Spolehlivost | ne |

### Successor a Feasible Successor

- **Successor** – nejlepší cesta, je ve směrovací tabulce
- **Feasible Successor** – ověřená záložní cesta, drží se v topologické tabulce

Když hlavní cesta vypadne, EIGRP okamžitě nasadí zálohu **bez přepočítávání** – proto je tak rychlý.

### Srovnání směrovacích protokolů

| | RIP | **EIGRP** | [[OSPF]] | [[BGP]] |
| :-- | :-- | :-- | :-- | :-- |
| Typ | distance vector | hybridní | link-state | path vector |
| Výrobce | otevřený | Cisco | otevřený | otevřený |
| Metrika | počet hopů | šířka pásma + zpoždění | cost | politiky |
| Použití | malé sítě | Cisco sítě | velké sítě | internet |

### Čísla, která se hodí znát

| Co | Hodnota |
| :-- | :-- |
| administrativní vzdálenost | 90 (interní), 170 (externí) |
| Hello / Hold časovač | 5 s / 15 s (na rychlých linkách) |
| multicast adresa | 224.0.0.10 |
| algoritmus | **DUAL** |
| označení v `show ip route` | **D** |

### Základní konfigurace

```
R1(config)# router eigrp 100
R1(config-router)# network 192.168.10.0 0.0.0.255
R1(config-router)# network 10.0.0.0 0.0.0.3
R1(config-router)# no auto-summary
```

- `100` je **číslo AS**. Na rozdíl od OSPF musí být **stejné na všech routerech**, jinak se nestanou sousedy,
- `no auto-summary` vypne automatické shrnování podle tříd.

### Ověření

`show ip eigrp neighbors`, `show ip route eigrp`, `show ip eigrp topology` (successors a feasible successors).

### Dostupnost

EIGRP byl dlouho jen Cisco. V roce 2013 Cisco zveřejnilo jeho základní část, v roce 2016 vyšla jako RFC 7868. V praxi ho stejně používají hlavně sítě s Cisco zařízeními.

**Souvisí:** [[OSPF]], [[BGP]], [[router]], [[VLSM]], [[multicast]]
