---
aliases: [broadcast domain]
tags: [slovnik]
---

# broadcast doména

**Broadcast doména** – oblast sítě, kam se šíří [[broadcast]]. Příklad: všechny propojené switche v jedné LAN tvoří jednu broadcast doménu.

---

## Podrobně

- sada propojených přepínačů = **jedna** broadcast doména,
- propojením dvou switchů se doména **zvětší**,
- vrstvu 2 rozdělí jen zařízení síťové vrstvy, např. [[router]],
- moc broadcastů = zbytečně vytížená šířka pásma, přetížení a zpomalení sítě,
- viz také segmentace v [[IPv4_adresovani]] (Network Segmentation).

### Jak spočítat broadcast domény

- každé **rozhraní routeru** = samostatná broadcast doména,
- každá **VLAN** = samostatná broadcast doména,
- switch ani hub broadcast doménu nerozdělí.

Příklad: router se dvěma LAN porty, na každém switch s PC → **2 broadcast domény**. Když na jednom switchi uděláš 3 VLAN → domén je víc podle počtu VLAN.

### Broadcast doména vs. kolizní doména

| | Kolizní doména | Broadcast doména |
| :-- | :-- | :-- |
| rozdělí | switch (každý port), router | jen router (nebo VLAN) |
| hub | jedna pro všechny porty | jedna |
| switch | každý port vlastní | celý switch jedna (bez VLAN) |

### Co v ní běží broadcastem

[[ARP]] Request, [[DHCP]] Discover a Request, některé ohlášení služeb. Čím víc zařízení v doméně, tím víc broadcastů musí každé zařízení přijmout a zpracovat.

**Souvisí:** [[broadcast]], [[kolizní doména]], [[router]], [[switch]], [[Koncepty_prepinani]]
