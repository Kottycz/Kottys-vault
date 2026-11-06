---
aliases: [-T0, -T4, timing, --min-rate, --max-rate, paralelismus]
tags: [slovnik]
---

# Časování skenování (`-T`)

Nastavení **rychlosti** skenu – profily `-T0` až `-T5`.

*Příklad: `nmap -T4 MACHINE_IP`.*

---

## Podrobně

- 0 paranoid, 1 sneaky, 2 polite, 3 normal (výchozí), 4 aggressive, 5 insane
- `-T0` čeká 5 min mezi sondami (proti [[IDS]])
- `-T4` pro CTF, `-T1` pro reálné testy
- `--min-rate` / `--max-rate` – pakety za sekundu
- `--min-parallelism` / `--max-parallelism` – paralelní sondy

**Souvisí:** [[IDS]], [[skenování portů]], [[nmap]]
