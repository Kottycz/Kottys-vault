---
aliases: [Wide Area Network, rozlehlá síť]
tags: [slovnik]
---

# WAN

**Wide Area Network** – rozlehlá síť propojující vzdálené lokality (města, země, kontinenty). Provozují ji poskytovatelé, organizace si její kapacitu pronajímá.

---

## Podrobně

### Charakteristika

- **Rozsah** – neomezený (města, státy, kontinenty)
- **Rychlost** – obvykle nižší než [[LAN]], vyšší [[latency|latence]]
- **Vlastnictví** – patří poskytovatelům (ISP, telekomunikační operátoři)
- **Účel** – propojit vzdálené pobočky nebo připojit LAN k internetu

Internet je vlastně největší WAN na světě.

### Technologie

| Technologie | Popis |
| :-- | :-- |
| **Optika** | vysoká rychlost, páteřní spoje |
| **DSL / VDSL** | přes telefonní linku |
| **Kabelový internet** | přes koaxiál (TV rozvody) |
| **Mobilní sítě** | 4G / 5G |
| **Satelitní** | odlehlé lokality, vysoká latence |
| **MPLS** | pronajaté okruhy pro firmy |
| **VPN** | šifrovaný tunel přes internet (levnější náhrada pronajatých linek) |

### Připojení LAN k WAN

Na hranici stojí [[router]] – jeho **WAN port** míří k poskytovateli, **LAN porty** do vnitřní sítě. Obvykle na něm běží i [[NAT]], aby se vnitřní privátní adresy přeložily na veřejnou.

### Terminologie u poskytovatele

- **ISP** (Internet Service Provider) – poskytovatel připojení
- **CPE** – zařízení u zákazníka (modem, router od poskytovatele)
- **Poslední míle** – úsek od sítě poskytovatele k zákazníkovi

### WAN vs. internet

Internet je největší WAN na světě, ale firma může mít i **soukromou WAN** – pronajaté linky od poskytovatele jen mezi svými pobočkami (MPLS, pronajatý okruh). Dnes se často místo nich používá internet + [[VPN]] (levnější) nebo SD-WAN.

### Topologie WAN

| Topologie | Popis |
| :-- | :-- |
| point-to-point | jedna linka mezi dvěma místy |
| hub-and-spoke | pobočky připojené jen k centrále |
| full mesh | každé místo propojené s každým, drahé, ale odolné |
| dual-homed | připojení ke dvěma poskytovatelům |

### Kde končí odpovědnost

**Demarcation point** (demarc) je místo, kde končí zařízení poskytovatele a začíná zákazníkovo. Problém před demarcem řeší [[ISP]], za ním zákazník.

**Souvisí:** [[LAN]], [[router]], [[NAT]], [[latency]], [[throughput]]
