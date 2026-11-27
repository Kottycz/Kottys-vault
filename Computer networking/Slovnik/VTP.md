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

### Režimy VTP

| Režim | Chování |
| :-- | :-- |
| **server** | vytváří, mění a maže VLAN, posílá je ostatním (výchozí režim) |
| **client** | VLAN nemění, přebírá je od serveru |
| **transparent** | VTP nepoužívá, jen přeposílá VTP zprávy dál, VLAN si spravuje sám |

### Podmínky synchronizace

- switche musí mít **stejnou VTP doménu** (`vtp domain SKOLA`),
- stejné heslo, pokud je nastavené,
- propojení přes **trunk**.

### Revision number – nebezpečí

Každá změna zvýší **revision number**. Switch přijme databázi s vyšším číslem. Když do sítě připojíš starý switch ze skladu s vyšším revision number, může **přepsat a smazat VLAN v celé síti**. Proto se doporučuje režim **transparent**, nebo před připojením číslo vynulovat (změnou domény).

### Příkazy

```
S1(config)# vtp mode transparent
S1(config)# vtp domain SKOLA
S1# show vtp status
```

**Souvisí:** [[VLAN]], [[VLAN trunk]], [[switch]], [[flash]]
