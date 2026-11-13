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

**Souvisí:** [[VLAN trunk]], [[VLAN]], [[switch]], [[802.1Q]], [[příkazy show]]
