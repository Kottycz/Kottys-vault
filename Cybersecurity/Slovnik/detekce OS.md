---
aliases: [-O, OS detection]
tags: [slovnik]
---

# Detekce OS (`-O`)

Odhad **operačního systému** cíle podle chování TCP/IP.

*Příklad: `sudo nmap -sS -O MACHINE_IP`.*

---

## Podrobně

- potřebuje ≥ 1 otevřený a ≥ 1 zavřený port
- je to **odhad** – verze může být špatně, virtualizace zkresluje
- `--traceroute` ukáže trasu k cíli

**Souvisí:** [[detekce služeb]], [[traceroute]], [[nmap]], [[fingerprinting]]
