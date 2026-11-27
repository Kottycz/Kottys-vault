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

### Konfigurace na Cisco routeru

```
R1(config)# ipv6 unicast-routing
R1(config)# interface g0/0/0
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64
R1(config-if)# no shutdown
```

`ipv6 unicast-routing` zapne směrování IPv6 a router začne posílat [[RA]] zprávy, ze kterých si klienti udělají vlastní GUA přes [[SLAAC]].

### Rozdělení prefixu

Typické přidělení od [[ISP]]:

```
2001:db8:acad::/48         ← global routing prefix (od ISP)
2001:db8:acad:0001::/64    ← subnet ID (1. podsíť)
2001:db8:acad:0002::/64    ← 2. podsíť
...                          16 bitů subnet ID = 65 536 podsítí
```

Rozhraní má vždy `/64`, zbylých **64 bitů je ID rozhraní**.

### Dokumentační prefix

`2001:db8::/32` je vyhrazený pro **příklady a dokumentaci** (v učebnicích, v Cisco kurzu). Na internetu se nesměruje.

**Souvisí:** [[IPv6]], [[ULA]], [[LLA]], [[SLAAC]], [[délka prefixu]], [[NAT]]
