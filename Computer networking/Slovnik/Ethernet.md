---
aliases: [IEEE 802.3]
tags: [slovnik]
---

# Ethernet

**Ethernet** – nejrozšířenější technologie **kabelových sítí [[LAN]]** (standard [[IEEE]] 802.3). Určuje, jak se posílají rámce po kabelu. Příklad: UTP kabel mezi PC a switchem je Ethernet.

---

## Podrobně

### Co definuje

- formát **rámce** (MAC adresy, [[EtherType]], data, [[FCS]]),
- přístup k médiu (dříve [[CSMA-CD]], dnes na switchích [[full-duplex]] bez kolizí),
- fyzické vrstvy: [[UTP]] kabel, [[optické vlákno]].

### Rychlosti

| Název | Rychlost | Typ |
| :-- | :-- | :-- |
| Ethernet | 10 Mb/s | |
| Fast Ethernet | 100 Mb/s | FastEthernet na portech Cisco |
| Gigabit Ethernet | 1 Gb/s | GigabitEthernet |

### Rámec

- minimum **64 B** (menší = [[runt]]),
- maximum **1 518 B** (větší = [[giant]]),
- kontrola chyb přes [[FCS]] / [[CRC]].

### Standardy

| Standard | Rychlost | Médium |
| :-- | :-- | :-- |
| 10BASE-T | 10 Mb/s | [[UTP]] Cat 3+ |
| 100BASE-TX | 100 Mb/s | UTP Cat 5 |
| 1000BASE-T | 1 Gb/s | UTP Cat 5e |
| 10GBASE-T | 10 Gb/s | UTP Cat 6a |
| 1000BASE-SX / LX | 1 Gb/s | [[optické vlákno]] (multimode / singlemode) |

V názvu: číslo = rychlost v Mb/s, BASE = baseband (jeden signál na médiu), za pomlčkou typ média (T = twisted pair).

### Dvě podvrstvy

Ethernet pracuje na vrstvě 1 a 2 [[OSI]]. Vrstva 2 se dělí na:

- [[LLC]] – komunikace se síťovou vrstvou,
- [[MAC podvrstva]] – adresování, zapouzdření, přístup k médiu.

### Velikost rámce

- minimum **64 B**, menší rámec je [[runt]],
- maximum **1518 B** (1522 s VLAN tagem), větší je [[giant]],
- data (payload) 46–1500 B, 1500 je výchozí [[MTU]].

**Souvisí:** [[IEEE]], [[MAC adresa]], [[duplex]], [[auto-negotiation]], [[switch]], [[runt]], [[giant]]
