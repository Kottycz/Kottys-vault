---
aliases: [Nmap, Network Mapper]
tags: [slovnik]
---

# Nmap

**Nmap (Network Mapper)** – open source nástroj pro mapování sítě: zjišťuje, které systémy jsou online a jaké služby na nich běží.

*Příklad: `nmap 10.11.12.15-20` prohledá 6 adres.*

---

## Podrobně

- autor **Gordon Lyon (Fyodor)**, první vydání **1997**, licence GPL
- průmyslový standard pro pentestery
- umí: zjišťování živých hostitelů, skenování portů, zjištění verzí služeb, detekci OS, traceroute, skripty (NSE)
- kroky skenování: cíle → [[zjišťování živých hostitelů|živí hostitelé]] → [[reverzní DNS]] → porty → verze → OS → traceroute → skripty → výstup

| Přepínač | Co dělá |
| :-- | :-- |
| `-iL soubor` | načte cíle ze souboru |
| `-sL` | jen vypíše cíle (reverzní DNS), neskenuje |
| `-n` | vypne dotazy na DNS |

**Souvisí:** [[zjišťování živých hostitelů]], [[arp-scan]], [[masscan]], [[reverzní DNS]]

**Další:** [[skenování portů]], [[detekce služeb]], [[detekce OS]], [[NSE]], [[výstupní formáty Nmap]], [[časování skenování]]
