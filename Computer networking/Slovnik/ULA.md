---
aliases: [Unique Local Address, unikátní lokální adresa]
tags: [slovnik]
---

# ULA

**Unique Local Address** – [[IPv6]] adresa pro vnitřní použití, která se nesměruje na internetu. Obdoba privátních adres v [[IPv4]]. Prefix **fc00::/7** (v praxi `fd00::/8`).

---

## Podrobně

### Struktura

```
fd  a1b2c3d4e5 : 0001 : 0000:0000:0000:0100
└┘  └─────────┘   └──┘   └─── ID rozhraní ───┘
prefix  náhodné    ID podsítě
        ID sítě
```

- **fd** – prefix pro lokálně přidělené ULA
- **Náhodné ID sítě (40 bitů)** – generuje se náhodně, aby při propojení dvou firem nedošlo ke kolizi adres
- **ID podsítě** – vlastní dělení sítě
- **ID rozhraní** – konkrétní zařízení

### Kde se používá

- Zařízení, která nemají chodit na internet (tiskárny, kamery, řídicí systémy)
- Vnitřní sítě, kde nechceš být závislý na prefixu od poskytovatele
- Testovací a laboratorní prostředí

### Výhoda oproti IPv4 privátním adresám

Privátní IPv4 rozsahy (192.168.x, 10.x) používá **každý**, takže při spojení dvou sítí (fúze firem, VPN) dochází ke kolizím. ULA má náhodných 40 bitů – pravděpodobnost kolize je zanedbatelná.

### ULA a NAT

ULA se **nepřekládá [[NAT|NATem]]** jako privátní IPv4. Když má zařízení chodit na internet, dostane vedle ULA ještě [[GUA]]. Zařízení tak má obvykle víc adres najednou.

### Srovnání

| Typ | Prefix | Kde platí |
| :-- | :-- | :-- |
| [[GUA]] | 2000::/3 | globálně (internet) |
| **ULA** | fc00::/7 | jen uvnitř organizace |
| [[LLA]] | fe80::/10 | jen v jednom segmentu |

**Souvisí:** [[IPv6]], [[GUA]], [[LLA]], [[NAT]], [[délka prefixu]]
