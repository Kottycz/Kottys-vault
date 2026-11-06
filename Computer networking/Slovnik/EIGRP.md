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

**Souvisí:** [[OSPF]], [[BGP]], [[router]], [[VLSM]], [[multicast]]
