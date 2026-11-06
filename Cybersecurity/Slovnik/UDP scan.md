---
aliases: [-sU]
tags: [slovnik]
---

# UDP scan (`-sU`)

Sken [[UDP]] portů. UDP nemá spojení ani handshake.

*Příklad: `sudo nmap -sU MACHINE_IP`.*

---

## Podrobně

- žádná odpověď = port **open|filtered**
- [[ICMP]] type 3 code 3 (port unreachable) = zavřený
- je **velmi pomalý** (1000 portů trvalo přes 1000 s)
- lze kombinovat s TCP scanem

**Souvisí:** [[skenování portů]], [[UDP]], [[ICMP]], [[stavy portů]], [[nmap]]
