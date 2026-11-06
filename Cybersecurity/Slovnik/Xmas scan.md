---
aliases: [-sX, vánoční strom]
tags: [slovnik]
---

# Xmas scan (`-sX`)

Nastaví současně [[FIN]], [[PSH]] a [[URG]] – paket „svítí jako vánoční strom“.

*Příklad: `sudo nmap -sX MACHINE_IP`.*

---

## Podrobně

- zavřený port odpoví [[RST]]
- jinak `open|filtered`
- účinný proti bezstavovému firewallu

**Souvisí:** [[skenování portů]], [[Null scan]], [[FIN scan]], [[FIN]], [[PSH]], [[URG]], [[RST]]
