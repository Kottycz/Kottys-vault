---
aliases: [ping scan, -sn, ping sweep]
tags: [slovnik]
---

# ping scan (`-sn`)

Režim [[nmap|Nmapu]], který **jen zjistí živé hostitele** a **neskenuje jejich porty**.

*Příklad: `nmap -sn 10.10.68.220/24` vypíše, kteří z 256 adres jsou online.*

---

## Podrobně

- přepínač **`-sn`** (dřív `-sP`)
- Nmap ve výchozím nastavení dělá nejdřív ping scan a teprve potom skenuje porty živých hostitelů
- kombinuje se s přepínači, které určují **metodu**:

| Přepínač | Metoda |
| :-- | :-- |
| `-PR` | jen [[ARP]] (stejná podsíť) |
| `-PE` | ICMP echo |
| `-PP` | [[ICMP timestamp]] |
| `-PM` | [[ICMP address mask]] |

- bez `-sn` by po zjištění živých hostitelů následovalo skenování portů

**Souvisí:** [[zjišťování živých hostitelů]], [[nmap]], [[ARP]], [[ICMP]]
