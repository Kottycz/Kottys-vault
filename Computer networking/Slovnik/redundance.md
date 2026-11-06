---
aliases: [redundantní, záloha, redundancy]
tags: [slovnik]
---

# redundance

**Záměrné zdvojení důležitých částí sítě** (zařízení, linek, cest), aby při výpadku jedné části síť fungovala dál.

---

## Podrobně

### K čemu slouží

Pro zachování vysokého stupně **spolehlivosti** je v návrhu sítě nutná redundance. Pomáhá eliminovat jednotlivé body selhání – viz [[single point of failure]].

### Příklady

| Co se zdvojí | Co se tím vyřeší |
| :-- | :-- |
| druhý uplink mezi [[switch\|switchi]] | výpadek jednoho kabelu |
| druhý [[router]] | porucha routeru |
| záložní připojení k [[ISP\|poskytovateli]] | výpadek internetu |
| záložní napájení | výpadek proudu |

### Pozor na smyčky

Když jsou mezi switchi dvě cesty, vznikne v síti smyčka. Aby smyčka síť nezahltila, používá se [[STP protokol]], který redundantní linku drží vypnutou a zapne ji, až když hlavní cesta selže.

### Cena

Redundance **stojí peníze** – další zařízení, kabeláž, správa. U malé sítě se proto zdvojují jen nejdůležitější části.

**Souvisí:** [[single point of failure]], [[škálování sítě]], [[STP protokol]], [[switch]], [[router]]
