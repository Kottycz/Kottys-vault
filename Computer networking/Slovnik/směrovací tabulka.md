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

### Ukázka výpisu

```
R1# show ip route
Gateway of last resort is 203.0.113.1 to network 0.0.0.0

S*    0.0.0.0/0 [1/0] via 203.0.113.1
      192.168.1.0/24 is variably subnetted, 2 subnets, 2 masks
C        192.168.1.0/24 is directly connected, GigabitEthernet0/0/0
L        192.168.1.1/32 is directly connected, GigabitEthernet0/0/0
O     10.10.10.0/24 [110/2] via 192.168.12.2, 00:05:12, GigabitEthernet0/0/1
```

Čtení řádku s OSPF:

| Část | Význam |
| :-- | :-- |
| `O` | naučeno přes [[OSPF]] |
| `10.10.10.0/24` | cílová síť |
| `[110/2]` | AD 110 / metrika 2 |
| `via 192.168.12.2` | next hop |
| `00:05:12` | jak dlouho cesta existuje |
| `GigabitEthernet0/0/1` | výstupní rozhraní |

### Statická cesta

```
R1(config)# ip route 10.20.0.0 255.255.0.0 192.168.12.2
R1(config)# ip route 0.0.0.0 0.0.0.0 203.0.113.1
```

Druhý řádek je **výchozí cesta** – kam poslat vše, co router nezná.

### IPv6

`show ipv6 route`, statická cesta `ipv6 route 2001:db8:b::/64 2001:db8:12::2`.

**Souvisí:** [[router]], [[IPv4]], [[IPv6]], [[délka prefixu]], [[default gateway]], [[příkazy show]]
