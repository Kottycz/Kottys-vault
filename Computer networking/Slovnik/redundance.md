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

### Redundance na různých vrstvách

| Vrstva | Řešení |
| :-- | :-- |
| linky mezi switchi | víc linek, [[STP protokol|STP]] hlídá smyčky, nebo EtherChannel (svazek linek) |
| brána | FHRP (HSRP, VRRP) – dva routery sdílí jednu IP brány |
| připojení k internetu | dva [[ISP]] |
| napájení | dva zdroje, [[RPS]], UPS |
| servery | cluster, zálohy |

### EtherChannel

Několik fyzických linek mezi dvěma switchi se spojí do **jedné logické**. Sečte se šířka pásma a výpadek jedné linky nic nepřeruší. STP je bere jako jednu linku, takže je neblokuje.

### HSRP v kostce

Dva routery mají vlastní IP adresy a sdílí **virtuální IP** a virtuální MAC. PC mají jako bránu virtuální IP. Aktivní router provoz obsluhuje, záložní čeká, a když aktivní vypadne, převezme virtuální IP.

**Souvisí:** [[single point of failure]], [[škálování sítě]], [[STP protokol]], [[switch]], [[router]]
