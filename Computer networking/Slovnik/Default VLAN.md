---
aliases: [výchozí VLAN, VLAN 1]
tags: [slovnik]
---

# Default VLAN

**Default VLAN** – [[VLAN]], do které patří všechny porty switche, dokud je nepřiřadíš jinam. Je to **VLAN 1**. Příklad: nový switch z krabice, všechny porty jsou ve VLAN 1.

---

## Podrobně

- po zapnutí jsou všechny porty ve VLAN 1, proto se všechna zařízení na novém switchi vidí,
- VLAN 1 je zároveň výchozí [[nativní VLAN]] pro [[VLAN trunk|trunky]],
- Cisco ji nejde smazat ani přejmenovat,
- z bezpečnostních důvodů se pro běžný provoz nepoužívá, vytvoří se vlastní [[Data VLAN|datové VLAN]].

### Co ve VLAN 1 běží

Kromě uživatelského provozu jde ve VLAN 1 i řídicí provoz switchů: [[CDP]], [[VTP]], [[DTP]], [[STP protokol|STP]]. Proto je VLAN 1 pro útočníka zajímavá.

### Doporučení

| Co | Dát do |
| :-- | :-- |
| uživatelská zařízení | vlastní [[Data VLAN]] (10, 20, …) |
| správu switchů | [[Management VLAN]] (např. 99) |
| [[nativní VLAN]] trunku | nepoužívaná VLAN (např. 999) |
| nepoužité porty | „parkovací" VLAN, vypnuté (`shutdown`) |

### Ověření

`show vlan brief` – na novém switchi uvidíš ve VLAN 1 (default) všechny porty a VLAN 1002–1005, které jsou vyhrazené pro staré technologie (Token Ring, FDDI) a nejde je smazat.

**Souvisí:** [[VLAN]], [[nativní VLAN]], [[Data VLAN]], [[Management VLAN]], [[VLAN trunk]]
