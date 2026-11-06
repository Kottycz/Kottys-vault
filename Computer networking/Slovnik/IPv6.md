---
aliases: [Internet Protocol version 6]
tags: [slovnik]
---

# IPv6

**Internet Protocol version 6** – nástupce [[IPv4]] se **128bitovou** adresou, zapisovanou jako osm skupin hexadecimálních čísel oddělených dvojtečkami.

---

## Podrobně

### Proč vznikl

IPv4 má jen ~4,3 miliardy adres a ty došly. IPv6 má 128 bitů = 340 undecilionů adres – prakticky nevyčerpatelné množství.

### Zápis adresy

```
2001:0db8:0000:0000:0000:ff00:0042:8329
```

Osm [[hextet|hextetů]] (skupin po 16 bitech, 4 hexadecimální znaky).

**Zkracování:**
1. Vynechat úvodní nuly v hextetu: `0042` → `42`
2. Nahradit jednu souvislou skupinu nulových hextetů dvojtečkou `::` (jen jednou v adrese!)

```
2001:0db8:0000:0000:0000:ff00:0042:8329
2001:db8:0:0:0:ff00:42:8329          (krok 1)
2001:db8::ff00:42:8329               (krok 2)
```

### Struktura

```
2001:0db8:acad : 0001 : 0000:0000:0000:0100
└── prefix (64 b) ──┘  └─ ID rozhraní (64 b) ─┘
```

Standardní [[délka prefixu]] pro síť je **/64**.

### Typy adres

| Typ | Prefix | Použití |
| :-- | :-- | :-- |
| **[[GUA]]** | 2000::/3 | globální, směrovatelná na internetu (obdoba veřejné IPv4) |
| **[[ULA]]** | fc00::/7 | lokální, nesměrovatelná (obdoba privátní IPv4) |
| **[[LLA]]** | fe80::/10 | link-local, jen v rámci jednoho segmentu, má ji každé rozhraní |
| **Loopback** | ::1 | sám sobě |
| **[[multicast]]** | ff00::/8 | skupinové vysílání |

### Co v IPv6 není

- **[[broadcast]]** – nahrazuje ho multicast (efektivnější)
- **[[ARP]]** – nahrazuje ho [[NDP]] (zprávy [[RS]], [[RA]], [[NS]], NA)
- **[[NAT]]** – není potřeba, adres je dost

### Získání adresy

- **[[SLAAC]]** – zařízení si adresu vytvoří samo z prefixu v [[RA]] zprávě od [[router|routeru]]
- **DHCPv6** – přidělí server, jako u IPv4
- **Staticky** – ručně

Před použitím si zařízení ověří, že adresu nemá nikdo jiný, pomocí [[DAD]].

**Souvisí:** [[IPv4]], [[hextet]], [[GUA]], [[ULA]], [[LLA]], [[SLAAC]], [[NDP]], [[EUI-64]], [[DAD]]
