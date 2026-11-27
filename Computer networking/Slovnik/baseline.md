---
aliases: [baseline, network baseline, základní výkon sítě]
tags: [slovnik]
---

# baseline

**Baseline** – záznam běžného výkonu sítě, se kterým se pak porovnává aktuální stav.

*Příklad: síť je občas pomalá → podle baseline zjistím, jestli je to normální špička, nebo problém.*

---

## Podrobně

- měří se: odezva ([[ping]]), [[throughput]], vytížení linek, chybovost
- měří se **dlouhodobě a v různé denní doby**
- slouží k:
  - odhalení problému (odchylka od normálu)
  - plánování rozšíření sítě
- vytváří se po postavení sítě a pravidelně se aktualizuje

### Co a jak měřit

| Co | Čím |
| :-- | :-- |
| odezva a ztráty | [[ping]], [[traceroute]] |
| vytížení linek, chyby | `show interfaces` (input/output rate, CRC, collisions) |
| vytížení CPU a paměti | `show processes cpu`, `show memory` |
| dlouhodobé grafy | monitorovací software (SNMP, NetFlow) |
| obsah provozu | [[Wireshark]] |

### Jak se použije při problému

Uživatelé hlásí, že je síť pomalá. Bez baseline nevíš, jestli je 40 % vytížení linky hodně, nebo běžné. S baseline vidíš, že normálně je linka v tuhle hodinu na 15 %, takže 40 % je opravdu problém, a víš, kde hledat.

### Kdy ji aktualizovat

Po každé větší změně v síti (nový server, víc uživatelů, nová linka), jinak porovnáváš se stavem, který už neplatí.

**Souvisí:** [[ping]], [[throughput]], [[latency]]
