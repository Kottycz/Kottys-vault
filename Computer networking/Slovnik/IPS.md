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

**Souvisí:** [[firewall]], [[VPN]], [[DoS-DDoS]]
