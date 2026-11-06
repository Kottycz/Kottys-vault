---
aliases: [Virtual LAN, virtuální síť]
tags: [slovnik]
---

# VLAN

**Virtual LAN** – logické rozdělení jednoho [[switch|switche]] na několik oddělených sítí. Zařízení v různých VLAN se navzájem nevidí, i když jsou na stejném switchi.

---

## Podrobně

### K čemu

```
Jeden fyzický switch:

Porty 1–8   → VLAN 10 (kanceláře)
Porty 9–16  → VLAN 20 (výroba)
Porty 17–24 → VLAN 30 (hosté)
```

Místo tří samostatných switchů stačí jeden. Každá VLAN je vlastní **broadcastová doména** – [[broadcast]] z VLAN 10 se do VLAN 20 nedostane.

### Výhody

- **Bezpečnost** – oddělení oddělení, hosté nevidí firemní data
- **Menší broadcast provoz** – doména je menší
- **Flexibilita** – přesun zařízení jinam neznamená přepojování kabelů, stačí změnit VLAN portu
- **Úspora** – jeden switch místo několika

### Typy portů

| Typ | Popis |
| :-- | :-- |
| **Access port** | patří jedné VLAN, vede ke koncovému zařízení |
| **Trunk port** | přenáší víc VLAN najednou, vede mezi switchi nebo na [[router]] |

Na trunku se rámce **označkují** podle standardu [[IEEE]] **802.1Q** – přidá se 4bajtová značka s číslem VLAN, aby druhá strana věděla, kam rámec patří.

### Komunikace mezi VLAN

VLANy jsou oddělené sítě, takže mezi nimi musí směrovat vrstva 3:

- **Router-on-a-stick** – jeden trunk na [[router]] s podrozhraními
- **L3 switch** – směruje sám pomocí [[SVI]] pro každou VLAN

### VLAN 1

Výchozí VLAN, do které patří všechny porty. Z bezpečnostních důvodů se **nepoužívá** pro provoz ani správu – vytvoří se vlastní.

**Souvisí:** [[switch]], [[broadcast]], [[SVI]], [[router]], [[IEEE]], [[LAN]]
