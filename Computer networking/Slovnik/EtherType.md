---
aliases: [Type/Length, typ rámce]
tags: [slovnik]
---

# EtherType

**2bajtové pole v ethernetovém rámci**, které říká, jaký protokol vyšší vrstvy je uvnitř. Díky němu příjemce ví, komu obsah předat.

---

## Podrobně

### Umístění

```
[Preambule][SFD][Cíl MAC][Zdroj MAC][EtherType][Data][FCS]
                                        2 B
```

### Nejdůležitější hodnoty

| Hodnota | Protokol |
| :-- | :-- |
| **0x0800** | [[IPv4]] |
| **0x86DD** | [[IPv6]] |
| **0x0806** | [[ARP]] |
| 0x8100 | [[VLAN]] značka (802.1Q) |
| 0x8864 | PPPoE |

Tyhle tři první stojí za zapamatování – objevují se v testech i ve Wiresharku.

### Typ vs. délka

Pole má dvojí význam podle hodnoty:

- **≥ 1536 (0x0600)** – jde o **EtherType**, tedy typ protokolu (dnešní Ethernet II)
- **≤ 1500** – jde o **délku** dat (starší formát IEEE 802.3 s [[LLC]] hlavičkou)

Protože maximální délka dat je 1500 B, nedojde k záměně. V praxi se dnes používá skoro výhradně Ethernet II s EtherType.

### Proč je to potřeba

Bez tohoto pole by síťová karta nevěděla, jestli má obsah rámce předat IPv4 stacku, IPv6 stacku nebo ARP modulu – všechny běží zároveň nad stejným Ethernetem.

### Další hodnoty

| Hodnota | Protokol |
| :-- | :-- |
| `0x0800` | [[IPv4]] |
| `0x0806` | [[ARP]] |
| `0x86DD` | [[IPv6]] |
| `0x8100` | [[802.1Q]] VLAN tag |
| `0x88CC` | LLDP |
| `0x8847` | MPLS |

### Ve Wiresharku

Filtr podle EtherType: `eth.type == 0x0806` ukáže jen ARP. V detailu rámce je pole pod názvem **Type**.

**Souvisí:** [[MAC podvrstva]], [[LLC]], [[zapouzdření]], [[IPv4]], [[IPv6]], [[ARP]]
