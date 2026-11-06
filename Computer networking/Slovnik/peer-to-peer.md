---
aliases: [P2P, peer to peer, rovný s rovným]
tags: [slovnik]
---

# peer-to-peer

**Model sítě, kde je každé zařízení zároveň klientem i serverem.** Zařízení si poskytují služby navzájem, bez centrálního serveru.

---

## Podrobně

### Peer-to-peer vs. klient-server

| | peer-to-peer | klient-server |
| :-- | :-- | :-- |
| Role zařízení | každý je klient i server | oddělené role |
| Centrální prvek | není | server |
| Správa | na každém zařízení zvlášť | centrální |
| Cena | nízká | vyšší (server, licence) |
| Škálovatelnost | špatná (nad ~10 zařízení) | dobrá |
| Bezpečnost | slabá | řízená centrálně |
| Při výpadku | vypadne jen dané zařízení | vypadne vše |

### Kde se používá

**Malé sítě:**
- Domácí síť se sdílenou složkou nebo tiskárnou
- Malá kancelář bez serveru

**P2P aplikace (i přes internet):**
- **BitTorrent** – soubor se stahuje po kouscích od mnoha uživatelů zároveň
- **Blockchain** (kryptoměny) – žádný centrální registr
- Některé messengery a hovory (přímé spojení mezi účastníky)

### Výhody

- Jednoduché a levné – žádný server není potřeba
- Odolné – není jediný bod selhání
- U sdílení souborů se **s počtem uživatelů zrychluje** (víc zdrojů)

### Nevýhody

- **Správa nároste** – uživatele a práva musíš nastavit na každém zařízení zvlášť
- **Slabá bezpečnost** – žádná centrální kontrola
- **Výkon** – zařízení obsluhuje ostatní i při vlastní práci
- **Zálohování** – data jsou roztroušená všude

**Souvisí:** [[LAN]], [[socket]], [[port]]
