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

**Souvisí:** [[IEEE]], [[MAC adresa]], [[duplex]], [[auto-negotiation]], [[switch]], [[runt]], [[giant]]
