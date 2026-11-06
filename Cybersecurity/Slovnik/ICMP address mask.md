---
aliases: [ICMP address mask, ICMP maska adresy, -PM]
tags: [slovnik]
---

# ICMP address mask

Typ [[ICMP]] zprávy, kterým se hostitel ptá na **masku podsítě**; Nmap ho použije k zjištění, jestli je cíl online.

*Příklad: `nmap -PM -sn 10.10.68.220/24`.*

---

## Podrobně

| | Typ ICMP |
| :-- | :-- |
| požadavek na masku adresy | **17** |
| odpověď na masku adresy | **18** |

- přepínač Nmapu **`-PM`**
- v místnosti: **0 hostitelů** za 52,17 s, i když jich bylo aspoň 8 – paket **blokoval firewall na trase**
- každý požadavek se poslal **dvakrát** (vidět ve Wiresharku jako `Address mask request`)
- poučení: když je jeden typ paketu blokován, zkusím jiný ([[ICMP timestamp]], echo, TCP/UDP)

**Souvisí:** [[ICMP]], [[ICMP timestamp]], [[ping scan]], [[maska podsítě]], [[firewall]]
