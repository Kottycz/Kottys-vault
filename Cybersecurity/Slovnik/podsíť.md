---
aliases: [podsíť, subnet, podsítě]
tags: [slovnik]
---

# podsíť

Logická část sítě s vlastním rozsahem IP adres, k větší síti připojená přes **router**.

*Příklad: Network A = 10.1.100.0/24.*

---

## Podrobně

- obvykle jeden nebo víc [[segment sítě|segmentů]] spojených dohromady a nastavených na stejný router
- v každé podsíti může stát [[firewall]] vynucující zásady zabezpečení
- **[[ARP]] se nesměruje** – dotazy ARP zůstávají ve své podsíti, pro jinou podsíť jdou pakety přes výchozí bránu

| Prefix | Maska | Hostitelů |
| :-- | :-- | :-- |
| /16 | 255.255.0.0 | asi 65 tisíc |
| /24 | 255.255.255.0 | asi 253 |
| /30 | 255.255.255.252 | 4 adresy |

**Souvisí:** [[segment sítě]], [[maska podsítě]], [[délka prefixu]], [[ARP]]
