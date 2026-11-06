---
aliases: [spoofing IP, -S]
tags: [slovnik]
---

# IP spoofing (`-S`)

**Podvržení zdrojové IP adresy** v paketech.

*Příklad: `nmap -e NET_INTERFACE -Pn -S SPOOFED_IP MACHINE_IP`.*

---

## Podrobně

- odpověď jde na podvrženou adresu → útočník musí **sledovat provoz**
- potřeba `-e` (rozhraní) a `-Pn` (bez ping scanu)
- základ pro [[idle scan]] a [[decoy scan]]

**Souvisí:** [[MAC spoofing]], [[decoy scan]], [[idle scan]], [[IP adresa]], [[nmap]]
