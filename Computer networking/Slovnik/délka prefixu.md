---
aliases: [prefix length, CIDR, prefix]
tags: [slovnik]
---

# délka prefixu

**Zápis `/číslo` za adresou**, který říká, kolik bitů zleva tvoří **síťovou část**. Nahrazuje zápis [[maska podsítě|masky]] a používá se u [[IPv4]] i [[IPv6]].

---

## Podrobně

### Zápis (CIDR notace)

```
192.168.1.10 /24     ← 24 bitů = síť, zbylých 8 = hosty
2001:db8:acad:1::1 /64  ← 64 bitů = prefix, zbylých 64 = ID rozhraní
```

Ekvivalent u IPv4: `/24` = `255.255.255.0`

### Převod prefix ↔ maska

| Prefix | Maska | Hostů |
| :-- | :-- | :-- |
| /8 | 255.0.0.0 | 16 777 214 |
| /16 | 255.255.0.0 | 65 534 |
| /24 | 255.255.255.0 | 254 |
| /25 | 255.255.255.128 | 126 |
| /26 | 255.255.255.192 | 62 |
| /27 | 255.255.255.224 | 30 |
| /28 | 255.255.255.240 | 14 |
| /30 | 255.255.255.252 | 2 |

Počet hostů = 2^(32 − prefix) − 2

### Proč vznikla (CIDR)

Dřív se sítě dělily na pevné **třídy** (A = /8, B = /16, C = /24), což strašně plýtvalo adresami – firma se 300 počítači dostala celou třídu B (65 tisíc adres). **CIDR** (Classless Inter-Domain Routing) zavedl libovolnou délku prefixu, takže se přidělí přesně tolik, kolik je potřeba. Na to navazuje [[VLSM]].

### U IPv6

Standardní délka prefixu pro jednu síť je **/64** – zbylých 64 bitů je ID rozhraní (což potřebuje [[SLAAC]] a [[EUI-64]]). Poskytovatel typicky přiděluje /48 nebo /56, ze kterých si organizace nadělí jednotlivé /64 sítě.

**Souvisí:** [[maska podsítě]], [[VLSM]], [[IPv4]], [[IPv6]], [[IP adresa]]
