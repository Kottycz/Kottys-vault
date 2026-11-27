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

### Peer-to-peer aplikace vs. síť

- **P2P síť** – pár počítačů v kanceláři, které si sdílí složky a tiskárnu bez serveru,
- **P2P aplikace** – program, kde si klienti posílají data přímo mezi sebou, i když síť jinak funguje klient-server (BitTorrent, některé hlasové a video hovory).

### Kdy P2P síť stačí

Malá kancelář nebo domácnost s několika zařízeními. Od zhruba 10 a více zařízení je správa P2P nepřehledná (každý počítač má vlastní účty a oprávnění) a vyplatí se server.

### Bezpečnostní riziko

P2P aplikace otevírají spojení na mnoho neznámých počítačů. Přes sdílené soubory se šíří [[malware]] a může dojít k úniku dat, proto je firmy často blokují.

**Souvisí:** [[LAN]], [[socket]], [[port]]
