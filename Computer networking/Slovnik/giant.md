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

**Souvisí:** [[runt]], [[MTU]], [[CRC]], [[Ethernet]], [[příkazy show]]
