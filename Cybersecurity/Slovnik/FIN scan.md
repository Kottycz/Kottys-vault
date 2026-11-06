---
aliases: [-sF, TCP FIN]
tags: [slovnik]
---

# FIN scan (`-sF`)

Pošle paket s příznakem [[FIN]].

*Příklad: `sudo nmap -sF MACHINE_IP`.*

---

## Podrobně

- zavřený port odpoví [[RST]]
- jinak `open|filtered`
- některé firewally zahazují tiše

**Souvisí:** [[skenování portů]], [[Null scan]], [[Xmas scan]], [[FIN]], [[RST]], [[stavy portů]]
