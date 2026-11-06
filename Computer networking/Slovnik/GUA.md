---
aliases: [Global Unicast Address, globální unicast adresa]
tags: [slovnik]
---

# GUA

**Global Unicast Address** – globálně jedinečná a směrovatelná [[IPv6]] adresa. Obdoba veřejné [[IPv4]] adresy. Prefix **2000::/3** (adresy začínající 2 nebo 3).

---

## Podrobně

### Struktura

```
2001:0db8:acad : 0001 : 0000:0000:0000:0100
└─ globální prefix ┘ └ ID podsítě ┘ └─ ID rozhraní ─┘
      48 bitů          16 bitů           64 bitů
```

- **Globální směrovací prefix** – přiděluje poskytovatel (typicky /48)
- **ID podsítě** – organizace si z něj nadělí vlastní sítě (16 bitů = 65 536 podsítí)
- **ID rozhraní** – identifikuje konkrétní zařízení (64 bitů)

### Jak ji zařízení získá

- **[[SLAAC]]** – sestaví si ji samo z prefixu v [[RA]] zprávě (nejběžnější)
- **DHCPv6** – přidělí server
- **Staticky** – nastaví správce (servery, [[router|routery]])

Před použitím si ji zařízení ověří přes [[DAD]], jestli ji už nemá někdo jiný.

### Srovnání typů IPv6 adres

| Typ | Prefix | Směrovatelná | Obdoba v IPv4 |
| :-- | :-- | :-- | :-- |
| **GUA** | 2000::/3 | ano, globálně | veřejná adresa |
| **[[ULA]]** | fc00::/7 | jen vnitřně | privátní adresa (10.x, 192.168.x) |
| **[[LLA]]** | fe80::/10 | ne, jen v segmentu | 169.254.x (APIPA) |

### Proč není potřeba NAT

Adres je tolik, že **každé zařízení může mít vlastní veřejnou GUA** – včetně mobilu a lednice. [[NAT]] tedy odpadá a obnovuje se původní end-to-end princip internetu. Bezpečnost řeší firewall, ne skrývání za NAT.

### Zařízení má obvykle víc adres

Typicky zároveň GUA (pro internet) i [[LLA]] (pro komunikaci v segmentu) – to je v IPv6 normální.

**Souvisí:** [[IPv6]], [[ULA]], [[LLA]], [[SLAAC]], [[délka prefixu]], [[NAT]]
