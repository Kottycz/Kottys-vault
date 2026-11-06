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

**Souvisí:** [[IPv4]], [[IPv6]], [[router]], [[SVI]], [[RA]], [[směrovací tabulka]]
