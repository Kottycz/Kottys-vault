---
aliases: [TCP hlavička, TCP header]
tags: [slovnik]
---

# Hlavička TCP

Úvodní část TCP segmentu (min. 20 bajtů; RFC 793) s **porty, pořadovými čísly a příznaky**.

*Příklad: příznaky URG, ACK, PSH, RST, SYN, FIN.*

---

## Podrobně

- porty 16 bitů, sekvenční a potvrzovací číslo 32 bitů
- 6 příznaků: [[URG]], [[ACK]], [[PSH]], [[RST]], [[SYN]], [[FIN]]
- různé kombinace příznaků využívají skeny jako [[Null scan]] nebo [[Xmas scan]]

**Souvisí:** [[TCP]], [[SYN]], [[ACK]], [[RST]], [[FIN]], [[PSH]], [[URG]], [[hlavička IP]]
