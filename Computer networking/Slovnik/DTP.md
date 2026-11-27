---
aliases: [Dynamic Trunking Protocol, dynamic auto, nonegotiate]
tags: [slovnik]
---

# DTP

**DTP** (Dynamic Trunking Protocol) – protokol, kterým se dva sousední switche **dohodnou, jestli spolu spojí [[VLAN trunk|trunk]]**. Příklad: jeden port je `dynamic auto`, druhý v režimu trunk → trunk se vyjedná sám.

---

## Podrobně

- zrychluje konfiguraci, port lze nastavit na trunk, ne-trunk, nebo na vyjednávání se sousedem,
- funguje jen **point-to-point** mezi dvěma zařízeními,
- vyjednává jen tehdy, když je port na druhé straně v režimu trunk, který DTP podporuje,
- **switche jiných výrobců DTP nepodporují**,
- trunk do zařízení bez DTP: `switchport mode trunk` + `switchport nonegotiate` (switch nebude posílat rámce DTP),
- kontrola: `show dtp interfaces`.

### Režimy portu

| Režim | Chování |
| :-- | :-- |
| `switchport mode access` | nikdy trunk |
| `switchport mode trunk` | vždy trunk, posílá DTP |
| `switchport mode dynamic desirable` | aktivně se snaží trunk vyjednat |
| `switchport mode dynamic auto` | trunk udělá, jen když o něj soused požádá |
| `switchport nonegotiate` | vypne posílání DTP |

Výchozí režim u Cisco 2960 je **dynamic auto**.

### Výsledek kombinací

| | dynamic auto | dynamic desirable | trunk | access |
| :-- | :-- | :-- | :-- | :-- |
| **dynamic auto** | access | trunk | trunk | access |
| **dynamic desirable** | trunk | trunk | trunk | access |
| **trunk** | trunk | trunk | trunk | nefunkční |
| **access** | access | access | nefunkční | access |

Pozor: **auto + auto = access**. Dva nové switche spojené kabelem trunk samy neudělají.

### Bezpečnost

Útočník může z PC poslat DTP zprávy, vyjednat trunk a vidět provoz všech VLAN. Proto se na portech k uživatelům nastaví `switchport mode access` a na trunku `switchport nonegotiate`.

**Souvisí:** [[VLAN trunk]], [[VLAN]], [[switch]], [[802.1Q]], [[příkazy show]]
