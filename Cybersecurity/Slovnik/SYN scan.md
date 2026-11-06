---
aliases: [-sS, stealth scan, half-open scan]
tags: [slovnik]
---

# SYN scan (`-sS`)

Výchozí sken s root právy – pošle [[SYN]], po odpovědi **handshake přeruší** pomocí [[RST]].

*Příklad: `sudo nmap -sS MACHINE_IP`.*

---

## Podrobně

- SYN/ACK = otevřený, RST = zavřený
- rychlý a méně pravděpodobně zalogovaný
- nelze kombinovat s `-sV` (ten handshake dokončí)

**Souvisí:** [[skenování portů]], [[TCP connect scan]], [[SYN]], [[RST]], [[3-way handshake]], [[nmap]]
