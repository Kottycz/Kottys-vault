---
aliases: [routovací tabulka, routing table]
tags: [slovnik]
---

# směrovací tabulka

**Směrovací tabulka** – seznam sítí, které [[router]] zná, a **kudy** (kterým rozhraním / přes jakého souseda) se do nich dostat. Příklad: paket pro `192.168.10.55` router pošle ven rozhraním G0/0/0, protože síť `192.168.10.0/24` je tam přímo připojená.

---

## Podrobně

### Zobrazení

```
R1# show ip route
R1# show ipv6 route
```

### Kódy záznamů

| Kód | Význam |
| :-- | :-- |
| **C** | **connected** – síť přímo připojená k rozhraní (rozhraní musí být up/up) |
| **L** | **local** – adresa samotného rozhraní routeru (`/32` u [[IPv4]], `/128` u [[IPv6]]) |
| S | statická trasa |
| O | [[OSPF]] |
| D | [[EIGRP]] |

Na každé nakonfigurované rozhraní s adresou, které je up/up, vzniknou **dva záznamy**: **C** (celá síť) a **L** (adresa routeru).

### Jak router rozhoduje

1. Porovná cílovou adresu paketu se záznamy.
2. Vybere **nejdelší shodu prefixu** ([[délka prefixu]]).
3. Pokud nic nesedí a existuje výchozí trasa, použije ji; jinak paket zahodí.

### Odkud se tabulka plní

- **přímo připojené** sítě (C, L) – automaticky po `no shutdown` a nastavení adresy,
- **statické** trasy – ručně,
- **dynamické** protokoly ([[OSPF]], [[EIGRP]], [[BGP]]).

**Souvisí:** [[router]], [[IPv4]], [[IPv6]], [[délka prefixu]], [[default gateway]], [[příkazy show]]
