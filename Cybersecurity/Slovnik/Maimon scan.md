---
aliases: [-sM, TCP Maimon]
tags: [slovnik]
---

# Maimon scan (`-sM`)

Pošle paket s příznaky [[FIN]] + [[ACK]]; popsal ho **Uriel Maimon** (1996).

*Příklad: `sudo nmap -sM MACHINE_IP`.*

---

## Podrobně

- některé systémy odvozené od BSD paket u otevřeného portu zahodí
- dnes téměř **nefunguje** – většina cílů odpoví RST vždy
- všech 1000 portů vyjde jako zavřené

**Souvisí:** [[skenování portů]], [[FIN]], [[ACK]], [[RST]], [[ACK scan]]
