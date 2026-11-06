---
aliases: [plně duplexní]
tags: [slovnik]
---

# full-duplex

**Plně duplexní přenos** – obě strany můžou vysílat a přijímat **současně**. Na Ethernetu standard u [[switch|switchů]], kolize tam vůbec nevznikají.

---

## Podrobně

### Jak to funguje

Kroucený kabel ([[UTP]]) má víc párů vodičů – jeden pár se používá pro vysílání, druhý pro příjem. Data tak tečou oběma směry naráz bez toho, aby se rušila.

```
PC  ══ vysílání ══►  switch
    ◄══ příjem  ══
```

### Režimy přenosu

| Režim | Popis | Analogie |
| :-- | :-- | :-- |
| **Simplex** | jen jedním směrem | rozhlasové vysílání |
| **[[half-duplex]]** | oběma směry, ale střídavě | vysílačka ("přepínám") |
| **Full-duplex** | oběma směry současně | telefon |

### Proč zmizely kolize

Ve full-duplexu není o co soupeřit – každý směr má vlastní vodiče. Proto se u moderních switchů **vypíná [[CSMA-CD]]**, není potřeba.

Rychlost se tím teoreticky zdvojnásobí: gigabitový port zvládne 1 Gb/s v každém směru zároveň.

### Autonegotiation

Zařízení si při připojení automaticky domluví rychlost (10/100/1000 Mb/s) a duplex. Když se domluva nepovede (typicky při ručním nastavení jen na jedné straně), vznikne **duplex mismatch**:

- jedna strana jede full, druhá half
- síť funguje, ale strašně pomalu, s chybami a kolizemi
- klasický problém při ladění sítě

Proto se doporučuje nechat autonegotiation zapnutou na obou stranách.

**Souvisí:** [[half-duplex]], [[switch]], [[CSMA-CD]], [[UTP]], [[Auto-MDIX]]
