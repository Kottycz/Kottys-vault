---
aliases: [-sN, TCP Null]
tags: [slovnik]
---

# Null scan (`-sN`)

Pošle TCP paket **bez jakéhokoli příznaku**.

*Příklad: `sudo nmap -sN MACHINE_IP`.*

---

## Podrobně

- zavřený port odpoví [[RST]]
- otevřený/filtrovaný neodpoví → `open|filtered`
- funguje za **bezstavovým firewallem**, který hledá jen SYN

**Souvisí:** [[skenování portů]], [[FIN scan]], [[Xmas scan]], [[RST]], [[stavový firewall]], [[stavy portů]]
