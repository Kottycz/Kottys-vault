---
aliases: [giants]
tags: [slovnik]
---

# giant

**Giant** – [[Ethernet]] rámec **větší než 1 518 bajtů**, který se zahodí. Příklad: rámec o 2 000 B se na běžné lince zahodí jako giant.

---

## Podrobně

- Vidíš ho v `show interfaces` mezi **input errors**.
- Příčina: vadná síťová karta/ovladač, špatně nastavené **jumbo frames** na jedné straně, chyba zařízení.
- Opak: [[runt]] (rámec pod 64 B).
- Maximum 1 518 B = 1 500 B dat ([[MTU]]) + hlavička a [[FCS]].

### Proč je limit 1518 bajtů

| Část | Bajty |
| :-- | :-- |
| cílová MAC | 6 |
| zdrojová MAC | 6 |
| [[EtherType]] | 2 |
| data | max 1500 |
| [[FCS]] | 4 |
| **celkem** | **1518** |

S [[802.1Q]] tagem je maximum **1522 B**, takový rámec giant není.

### Jumbo rámce

Některé sítě (datová centra, úložiště) záměrně používají rámce až **9000 B** (jumbo frames), aby snížily režii. Musí to podporovat **všechna** zařízení na cestě. Když jedno jumbo neumí, bere ty rámce jako giant a zahazuje je.

### Co dělat, když gianty rostou

1. zkontrolovat nastavení MTU / jumbo na obou koncích,
2. vyměnit kabel a zkusit jiný port,
3. aktualizovat ovladač síťové karty nebo ji vyměnit.

**Souvisí:** [[runt]], [[MTU]], [[CRC]], [[Ethernet]], [[příkazy show]]
