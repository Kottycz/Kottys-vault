---
aliases: [duplexní režim]
tags: [slovnik]
---

# duplex

**Duplex** – způsob, jak spolu dvě zařízení na lince komunikují: buď **oba směry najednou** ([[full-duplex]]), nebo **střídavě** ([[half-duplex]]). Příklad: telefonní hovor je full-duplex, vysílačka („přepínám“) half-duplex.

---

## Podrobně

### Dva režimy

| | [[full-duplex]] | [[half-duplex]] |
| :-- | :-- | :-- |
| Směr | vysílá i přijímá **současně** | jen **jedním směrem** najednou |
| Kolize | žádné | ano, normální jev |
| Využití linky | 100 % v obou směrech | výrazně nižší |
| Kde | dnešní switche | staré huby |

### Nesoulad duplexu (duplex mismatch)

Jedna strana full, druhá half = **nejčastější tichý problém** na síti. Spojení „nějak“ funguje, ale je pomalé, a na half straně rostou [[late collision]] a [[CRC]] chyby. Příčina je obvykle selhání [[auto-negotiation]] nebo ruční nastavení jen na jedné straně.

### Nastavení na Cisco

```
S1(config)# interface FastEthernet 0/1
S1(config-if)# duplex full
S1(config-if)# speed 100
```

- 1000 Mb/s běží **jen full-duplex**.
- [[Optické vlákno|Optické porty]] jsou vždy full-duplex s pevnou rychlostí.
- Best practice: u známých zařízení (servery, switche, routery) nastavit **ručně na obou koncích**.

### Jak poznat mismatch v show interfaces

| Strana | Co roste |
| :-- | :-- |
| half-duplex strana | **late collisions**, collisions |
| full-duplex strana | **CRC** chyby, [[runt|runty]] |

Zároveň linka funguje, ale je velmi pomalá a ztrácí pakety, hlavně při větším provozu.

### Ověření

```
S1# show interfaces fa0/1 | include duplex
  Full-duplex, 100Mb/s, media type is 10/100BaseTX
S1# show interfaces status
```

Při kontrole vždy porovnej **oba konce** linky.

**Souvisí:** [[full-duplex]], [[half-duplex]], [[auto-negotiation]], [[kolize]], [[late collision]], [[Auto-MDIX]], [[Ethernet]]
