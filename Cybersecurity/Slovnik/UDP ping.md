---
aliases: [UDP ping, -PU]
tags: [slovnik]
---

# UDP ping (`-PU`)

Metoda [[nmap|Nmapu]], která pošle [[UDP]] paket na (pravděpodobně zavřený) port a čeká na **ICMP „port nedostupný"**.

*Příklad: `sudo nmap -PU -sn 10.10.68.220/24` → 5 živých hostitelů za 9,20 s.*

---

## Podrobně

| Stav portu | Reakce cíle |
| :-- | :-- |
| otevřený | **žádná odpověď** (nic se nestane) |
| zavřený | **ICMP Type 3, Code 3** (port nedostupný) → cíl je online |

- na otevřený port se odpověď nečeká, proto Nmap volí **neobvyklý port** (např. 40125), který je skoro jistě zavřený
- ICMP odpověď je **nepřímý důkaz**, že je hostitel online
- zadání portů stejně jako u [[TCP SYN ping]] (`-PU53`, `-PU1-100`)

**Souvisí:** [[TCP SYN ping]], [[TCP ACK ping]], [[ICMP]], [[UDP]], [[ping scan]], [[zjišťování živých hostitelů]]
