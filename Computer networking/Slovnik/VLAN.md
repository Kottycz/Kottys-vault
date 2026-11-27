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

### Rozsahy VLAN

| Rozsah | Význam |
| :-- | :-- |
| 1 | výchozí VLAN, nejde smazat |
| 2–1001 | normální rozsah, ukládá se do `vlan.dat` |
| 1002–1005 | vyhrazené pro staré technologie (Token Ring, FDDI) |
| 1006–4094 | rozšířený rozsah |

### Základní příkazy

```
S1(config)# vlan 10
S1(config-vlan)# name Kancelare
S1(config)# interface fa0/5
S1(config-if)# switchport mode access
S1(config-if)# switchport access vlan 10
S1# show vlan brief
```

### Typy VLAN

[[Default VLAN]], [[Data VLAN]], [[nativní VLAN]], [[Management VLAN]], [[Voice VLAN]]. Podrobně viz [[VLAN_cast_1]] a [[VLAN_cast_2]].

### Smazání VLAN – pozor

Když smažeš VLAN (`no vlan 10`), porty v ní **zůstanou přiřazené** k neexistující VLAN a přestanou fungovat. Nejdřív je přesuň do jiné VLAN.

**Souvisí:** [[switch]], [[broadcast]], [[SVI]], [[router]], [[IEEE]], [[LAN]]
