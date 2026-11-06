---
aliases: [runts]
tags: [slovnik]
---

# runt

**Runt** – [[Ethernet]] rámec **menší než 64 bajtů**, který se zahodí. Příklad: rámec o 40 B je runt, protože minimum pro Ethernet je 64 B.

---

## Podrobně

- Vidíš ho v `show interfaces` mezi **input errors**.
- Typická příčina: [[kolize]] (rámec se přeruší v půlce), vadná síťová karta nebo ovladač, [[duplex]] mismatch.
- Opak: [[giant]] (rámec nad 1 518 B).
- Několik runtů je normální po kolizi v [[half-duplex]], hodně runtů na [[full-duplex]] je chyba.

**Souvisí:** [[giant]], [[CRC]], [[kolize]], [[Ethernet]], [[příkazy show]]
