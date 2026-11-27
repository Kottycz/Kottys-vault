---
aliases: [dual stack, dualstack]
tags: [slovnik]
---

# dual-stack

**Dual-stack** – zařízení nebo síť, kde běží **[[IPv4]] i [[IPv6]] současně**. Příklad: rozhraní routeru má `192.168.10.1/24` i `2001:db8:acad:1::1/64` zároveň.

---

## Podrobně

### Proč

IPv4 postupně dochází a IPv6 ještě není všude. Dual-stack je **nejběžnější přechod** – zařízení mluví tím, co umí druhá strana.

### Konfigurace rozhraní routeru

```
R1(config)# interface gigabitethernet 0/0/0
R1(config-if)# ip address 192.168.10.1 255.255.255.0
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64
R1(config-if)# no shutdown
```

### Ověření

```
R1# show ip interface brief
R1# show ipv6 interface brief
```

### Poznámky

- Každý protokol má **vlastní** [[směrovací tabulka|směrovací tabulku]].
- Na [[switch]]i Catalyst 2960 s IOS 15.0 je pro IPv6 nutné `sdm prefer dual-ipv4-and-ipv6 default` a restart.
- Switch IPv6 [[default gateway]] nenastavuje – získá ji z [[RA]].

### Přechod z IPv4 na IPv6

| Metoda | Princip |
| :-- | :-- |
| **dual-stack** | IPv4 i IPv6 běží vedle sebe |
| **tunelování** | IPv6 pakety se zabalí do IPv4 a projdou přes IPv4 síť |
| **překlad (NAT64)** | zařízení jen s IPv6 komunikuje se zařízením jen s IPv4 přes překladač |

Dual-stack je doporučený způsob, protože nic nepřekládá a nic nebalí.

### Který protokol se použije

Když má cíl IPv4 i IPv6 adresu, operační systém ve výchozím stavu dá přednost **IPv6**.

### Na routeru nezapomenout

Aby router IPv6 pakety mezi sítěmi směroval, musí mít zapnuté `ipv6 unicast-routing`. Bez toho má rozhraní IPv6 adresy, ale pakety mezi sítěmi nepřeposílá.

**Souvisí:** [[IPv4]], [[IPv6]], [[router]], [[SVI]], [[RA]], [[směrovací tabulka]]
