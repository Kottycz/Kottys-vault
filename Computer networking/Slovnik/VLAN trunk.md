---
aliases: [trunk, trunk port, kmenová linka, VLAN Trunks]
tags: [slovnik]
---

# VLAN trunk

**VLAN trunk** – spoj mezi přepínači, kterým se šíří provoz **všech** [[VLAN]] najednou. Příklad: PC ve VLAN 10 na switchi A mluví s PC ve VLAN 10 na switchi B přes trunk, bez routeru.

---

## Podrobně

- zařízení na různých switchích, ale ve stejné VLAN, spolu komunikují bez [[router|routeru]],
- rámce na trunku se označují tagem podle [[802.1Q]],
- neoznačený rámec, který dorazí na trunk port, patří do [[nativní VLAN]].

**Souvisí:** [[VLAN]], [[802.1Q]], [[nativní VLAN]], [[switch]], [[router]]
