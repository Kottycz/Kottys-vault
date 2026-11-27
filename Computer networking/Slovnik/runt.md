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

### Proč je minimum 64 bajtů

Kvůli [[CSMA-CD]]: vysílající musí zjistit kolizi, ještě než dovysílá. Doba cesty signálu tam a zpátky přes síť je 512 bitů = 64 B. Kratší rámec by mohl skončit dřív, než se o kolizi dozví.

### Výplň (padding)

Když jsou data kratší než 46 B (např. malý [[ARP]] nebo [[TCP]] ACK), síťová karta je **doplní nulami**, aby rámec měl 64 B. Proto legitimní malý rámec runt není.

### Kde runty hledat

```
S1# show interfaces fa0/1
  0 runts, 0 giants, 0 throttles
  15 input errors, 12 CRC, 0 frame
```

Když jich přibývá na full-duplex lince, zkontroluj [[duplex]] na druhé straně a kabel.

**Souvisí:** [[giant]], [[CRC]], [[kolize]], [[Ethernet]], [[příkazy show]]
