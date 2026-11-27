---
aliases: [IPS, Intrusion Prevention System, IDS]
tags: [slovnik]
---

# IPS

**IPS (Intrusion Prevention System)** – systém, který sleduje síťový provoz, rozpozná útok a **sám ho zablokuje**.

*Příklad: IPS pozná podezřelý provoz z jedné IP adresy a začne ho zahazovat.*

---

## Podrobně

| | IDS | IPS |
| :-- | :-- | :-- |
| co dělá | útok **jen odhalí** a upozorní | útok odhalí a **zablokuje** |
| zapojení | mimo tok dat (kopie provozu) | přímo v toku dat (inline) |

- rozpoznává útoky podle známých vzorů (signatur) a neobvyklého chování
- v CCNA testu: **IPS a VPN** jsou typická bezpečnostní řešení pro firmy, ne pro domácnost

### IDS vs. IPS

| | IDS | IPS |
| :-- | :-- | :-- |
| zapojení | mimo cestu provozu (dostává kopii, např. ze SPAN portu) | **přímo v cestě** provozu (inline) |
| při útoku | jen **upozorní** | útok **zablokuje** |
| vliv na síť | žádný | zpomalí provoz, při chybě může zablokovat i legitimní provoz |

### Jak rozpoznává útok

- **podle signatur** – porovnává provoz se známými vzory útoků. Pozná známé útoky, nový neznámý útok mine,
- **podle anomálií** – naučí se, jak vypadá normální provoz ([[baseline]]), a hlásí odchylky. Pozná i nové útoky, ale dělá víc planých poplachů.

### Kde stojí

Typicky hned za [[firewall|firewallem]] na hranici sítě, dnes často jako součást firewallu nové generace (NGFW).

**Souvisí:** [[firewall]], [[VPN]], [[DoS-DDoS]]
