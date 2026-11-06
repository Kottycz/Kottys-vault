---
aliases: [Open Shortest Path First]
tags: [slovnik]
---

# OSPF

**Open Shortest Path First** – dynamický směrovací protokol. [[router|Routery]] si mezi sebou vyměňují informace o síti a každý si sám spočítá nejkratší cestu ke všem cílům.

---

## Podrobně

### Jak funguje

1. Routery si najdou **sousedy** (Hello zprávy na [[multicast]] 224.0.0.5)
2. Vymění si **LSA** (Link State Advertisements) – popis svých spojů a jejich cen
3. Každý router si z nich sestaví **stejnou mapu celé sítě** (link-state database)
4. Pomocí **Dijkstrova algoritmu** si spočítá nejkratší cestu ke každé síti
5. Nejlepší cesty zapíše do směrovací tabulky

### Metrika – cost

Cena spoje se odvozuje od **šířky pásma** (rychlejší linka = nižší cena). Protokol tedy preferuje rychlé cesty, ne nejkratší počet hopů.

```
cost = referenční šířka pásma / šířka pásma linky
```

### Oblasti (areas)

Ve velkých sítích se OSPF dělí na **oblasti**, aby routery nemusely počítat celou síť:

- **Area 0 (backbone)** – páteřní oblast, všechny ostatní se na ni napojují
- Ostatní oblasti komunikují mezi sebou jen přes Area 0

### Typy směrovacích protokolů

| Typ | Princip | Příklady |
| :-- | :-- | :-- |
| **Distance vector** | "soused mi řekl, jak daleko to je" | RIP, EIGRP |
| **Link state** | "znám mapu celé sítě, počítám sám" | **OSPF**, IS-IS |
| **Path vector** | cesty mezi autonomními systémy | BGP |

### Vlastnosti

- **Otevřený standard** (na rozdíl od Cisco EIGRP) – funguje napříč výrobci
- **Classless** – posílá i [[maska podsítě|masku]], podporuje [[VLSM]]
- **Rychlá konvergence** – na výpadek reaguje během vteřin
- **OSPFv2** pro [[IPv4]], **OSPFv3** pro [[IPv6]]

**Souvisí:** [[router]], [[VLSM]], [[multicast]], [[IP adresa]], [[maska podsítě]]
