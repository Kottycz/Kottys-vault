---
aliases: [-sI, zombie scan, zombie]
tags: [slovnik]
---

# Idle (zombie) scan (`-sI`)

Sken přes **nečinného hostitele (zombie)**; cíl vidí jen IP zombie.

*Příklad: `sudo nmap -sI ZOMBIE_IP MACHINE_IP`.*

---

## Podrobně

- útočník sleduje [[IP ID]] zombie
- rozdíl 1 = zavřený/filtrovaný, rozdíl 2 = otevřený
- zombie musí být opravdu **nečinný**
- využívá [[IP spoofing]]

**Souvisí:** [[IP ID]], [[IP spoofing]], [[skenování portů]], [[SYN]], [[RST]]
