---
aliases: [RST, Reset]
tags: [slovnik]
---

# RST (Reset)

Příznak [[TCP]], který **ukončí / odmítne spojení**.

*Příklad: SYN na zavřený port → cíl odpoví RST.*

---

## Podrobně

- zavřený port odpoví na [[SYN]] paketem **RST**
- na [[ACK]] mimo existující spojení cíl také odpoví **RST** (využívá [[TCP ACK ping]])
- pro Nmap je RST důkaz, že je hostitel **živý**

**Souvisí:** [[SYN]], [[ACK]], [[3-way handshake]], [[TCP SYN ping]], [[TCP ACK ping]]
