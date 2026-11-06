---
aliases: [-sT, connect scan]
tags: [slovnik]
---

# TCP connect scan (`-sT`)

Sken, který **dokončí celé [[3-way handshake]]** a pak spojení ukončí.

*Příklad: `nmap -sT MACHINE_IP`.*

---

## Podrobně

- jediná možnost **bez root/sudo**
- spolehlivý, ale **více viditelný** (spojení se může zalogovat)
- po handshaku odešle RST

**Souvisí:** [[skenování portů]], [[SYN scan]], [[3-way handshake]], [[RST]], [[nmap]]
