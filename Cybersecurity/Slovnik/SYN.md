---
aliases: [SYN, Synchronize]
tags: [slovnik]
---

# SYN (Synchronize)

Příznak v hlavičce [[TCP]], kterým se **zahajuje spojení** (první krok [[3-way handshake]]).

*Příklad: klient pošle SYN, server odpoví SYN/ACK, klient potvrdí [[ACK]].*

---

## Podrobně

- otevřený port odpoví **SYN/ACK**, zavřený [[RST]]
- Nmap ho využívá v [[TCP SYN ping]] (`-PS`) ke zjištění živých hostitelů

**Souvisí:** [[ACK]], [[RST]], [[3-way handshake]], [[TCP]]
