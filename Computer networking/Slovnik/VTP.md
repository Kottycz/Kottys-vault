---
aliases: [VLAN Trunking Protocol, VLAN trunking]
tags: [slovnik]
---

# VTP

**VTP** (VLAN Trunking Protocol) – protokol, který pomáhá **synchronizovat databázi [[VLAN]]** mezi přepínači. Příklad: VLAN se nastaví na jednom switchi a ostatní ji dostanou přes VTP.

---

## Podrobně

- konfigurace VLAN (normální rozsah 1–1005) se ukládají do souboru `vlan.dat` ve [[flash]] paměti switche,
- VTP pomáhá udržet tuto databázi stejnou na všech přepínačích,
- soubor `vlan.dat` jde smazat příkazem `delete flash:vlan.dat`.

**Souvisí:** [[VLAN]], [[VLAN trunk]], [[switch]], [[flash]]
