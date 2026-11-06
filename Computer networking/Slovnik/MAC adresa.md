---
aliases: [MAC address, fyzická adresa, hardwarová adresa]
tags: [slovnik]
---

# MAC adresa

**Media Access Control adresa** – 48bitová fyzická adresa síťové karty ([[NIC]]), zapisovaná hexadecimálně (`00:1A:2B:3C:4D:5E`). Pracuje na spojové vrstvě (OSI 2).

---

## Podrobně

### Struktura

48 bitů = 6 bajtů, rozdělených na dvě poloviny:

```
00:1A:2B : 3C:4D:5E
└─ OUI ─┘ └ sériové ┘
```

- **[[OUI]]** (24 bitů) – identifikátor výrobce
- **Zbytek** (24 bitů) – jedinečné číslo přidělené výrobcem

Díky OUI lze z MAC adresy vyčíst výrobce karty (Intel, Cisco, Apple…).

### MAC vs. IP adresa

| | MAC adresa | [[IP adresa]] |
| :-- | :-- | :-- |
| Vrstva | 2 (spojová) | 3 (síťová) |
| Rozsah platnosti | jen lokální síť | celý internet |
| Přiděluje | výrobce (natvrdo) | správce / [[DHCP]] |
| Mění se | ne (jde ale přepsat softwarově) | ano, podle sítě |
| Analogie | rodné číslo | adresa bydliště |

Rámec putuje mezi MAC adresami **uvnitř jedné sítě**; paket putuje mezi IP adresami **napříč sítěmi**. Při průchodu [[router|routerem]] se MAC adresy přepisují, IP adresy zůstávají.

### Jak se MAC zjistí

Když zařízení zná IP a potřebuje MAC, použije [[ARP]] (u [[IPv6]] je to [[NDP]]).

### Speciální adresy

- `FF:FF:FF:FF:FF:FF` – [[broadcast]], doručí se všem v síti
- Adresy začínající `01:00:5E` – IPv4 [[multicast]]
- Adresy začínající `33:33` – IPv6 multicast

### Jak ji switch používá

[[switch|Switch]] si buduje **MAC tabulku** – zapamatuje si, na kterém portu je která MAC adresa, a pak posílá rámce jen tam, kam patří (ne všem jako starý hub).

### Zobrazení

- Windows: `ipconfig /all`
- Linux: `ip link` nebo `ifconfig`

**Souvisí:** [[NIC]], [[OUI]], [[ARP]], [[switch]], [[IP adresa]], [[broadcast]], [[EUI-64]]
