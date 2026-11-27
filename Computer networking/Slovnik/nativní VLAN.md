---
aliases: [native VLAN]
tags: [slovnik]
---

# nativní VLAN

**Nativní VLAN** – [[VLAN]], do které se na trunk portu přiřadí **neoznačený** rámec. Standardně je to VLAN 1. Příklad: rámce pro správu mezi switchi jsou obvykle neoznačené.

---

## Podrobně

- určuje ji standard [[802.1Q]] pro kmenové ([[VLAN trunk|trunk]]) linky,
- výchozí hodnota: **VLAN 1**,
- neoznačený rámec na trunk portu = patří do nativní VLAN.

### Na co pozor

- **na obou koncích trunku musí být stejná** nativní VLAN. Když se liší, rámce bez tagu z jedné VLAN skončí na druhé straně v jiné VLAN. [[CDP]] to hlásí: `%CDP-4-NATIVE_VLAN_MISMATCH`,
- nativní VLAN se týká **jen trunk portů**, access port žádnou nativní VLAN nemá.

### Změna nativní VLAN

```
S1(config)# interface g0/1
S1(config-if)# switchport trunk native vlan 999
```

Ověření: `show interfaces trunk` (sloupec Native vlan).

### Proč ji měnit z VLAN 1

Útok **VLAN hopping s dvojitým tagem**: útočník ve VLAN, která je zároveň nativní, pošle rámec se dvěma tagy. První switch vnější tag odebere (je to nativní VLAN, tag se na trunk neposílá) a druhý switch podle vnitřního tagu pošle rámec do cizí VLAN. Když je nativní VLAN nepoužívaná a nejsou v ní žádní uživatelé, útok nefunguje.

**Souvisí:** [[VLAN]], [[VLAN trunk]], [[802.1Q]]
