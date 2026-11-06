---
aliases: [Router Advertisement]
tags: [slovnik]
---

# RA

**Router Advertisement** – zpráva [[NDP]], kterou [[router]] v [[IPv6]] oznamuje svoji přítomnost a posílá parametry sítě. Základ [[SLAAC]].

---

## Podrobně

### Kdy se posílá

- **Periodicky** – router ji rozesílá sám od sebe každých pár desítek sekund
- **Na vyžádání** – jako odpověď na [[RS]] (Router Solicitation) od zařízení, které se právě připojilo

Posílá se na [[multicast]] adresu `ff02::1` (všechna zařízení v segmentu).

### Co RA obsahuje

| Údaj | K čemu |
| :-- | :-- |
| **Prefix sítě** (např. 2001:db8:acad:1::/64) | zařízení si z něj složí adresu ([[SLAAC]]) |
| **[[LLA]] routeru** | použije se jako [[default gateway]] |
| **Příznaky M a O** | jestli má zařízení použít DHCPv6 |
| **[[MTU]]** | velikost rámce na segmentu |
| **Hop limit** | výchozí hodnota [[TTL]] |
| **Doby platnosti** | jak dlouho je prefix platný |

### Příznaky M a O

| M | O | Výsledek |
| :-- | :-- | :-- |
| 0 | 0 | čistý **SLAAC** – vše z RA |
| 0 | 1 | **stateless DHCPv6** – adresa ze SLAAC, DNS z DHCP |
| 1 | – | **stateful DHCPv6** – adresu přiděluje server |

### Bezpečnostní riziko: rogue RA

Kdokoliv v síti může poslat podvrženou RA a prohlásit se za router – provoz pak teče přes útočníka (man-in-the-middle). Někdy se to stane i omylem (zapnuté sdílení internetu na notebooku).

Obrana: **RA Guard** na [[switch|switchi]] – propouští RA jen z portů, kde je opravdu router.

**Souvisí:** [[RS]], [[NDP]], [[SLAAC]], [[IPv6]], [[LLA]], [[default gateway]], [[router]]
