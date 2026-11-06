---
aliases: [Local Area Network, lokální síť]
tags: [slovnik]
---

# LAN

**Local Area Network** – lokální síť na malém území (budova, patro, domácnost), spravovaná jedním subjektem. Typicky vysoká rychlost a nízká [[latency|latence]].

---

## Podrobně

### Charakteristika

- **Rozsah** – jedna budova nebo areál (desítky až stovky metrů)
- **Rychlost** – vysoká (1–10 Gb/s běžně)
- **Vlastnictví** – patří jedné organizaci/osobě, která ji celou spravuje
- **Technologie** – Ethernet (drát), Wi-Fi / WLAN (bezdrát)
- **Prvky** – [[switch|switche]], přístupové body, [[router]] na okraji

### Typy sítí podle rozsahu

| Zkratka | Název | Rozsah |
| :-- | :-- | :-- |
| **PAN** | Personal Area Network | pár metrů (Bluetooth) |
| **LAN** | Local Area Network | budova, areál |
| **MAN** | Metropolitan Area Network | město |
| **[[WAN]]** | Wide Area Network | země, kontinenty |
| **WLAN** | Wireless LAN | LAN bezdrátově (Wi-Fi) |
| **SAN** | Storage Area Network | síť pro úložiště |
| **VPN** | Virtual Private Network | šifrovaný tunel přes veřejnou síť |

### LAN vs. WAN

| | LAN | WAN |
| :-- | :-- | :-- |
| Rozsah | malý | velký |
| Rychlost | vysoká | obvykle nižší |
| Latence | nízká | vyšší |
| Vlastní | jedna organizace | poskytovatelé |
| Cena provozu | nízká | vysoká (pronájem linek) |

### Broadcastová doména

Celá LAN (přesněji jeden segment / VLAN) tvoří jednu **broadcastovou doménu** – [[broadcast]] se dostane ke všem. [[router|Router]] ji ohraničuje.

**Souvisí:** [[WAN]], [[switch]], [[router]], [[broadcast]], [[peer-to-peer]]
