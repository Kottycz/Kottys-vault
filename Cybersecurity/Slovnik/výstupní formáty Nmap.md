---
aliases: [-oN, -oG, -oX, -oA, -oS, výstup Nmap]
tags: [slovnik]
---

# Výstupní formáty Nmap

Možnosti, jak **uložit výsledky** skenu.

*Příklad: `nmap -sS -sV -O -oN scan MACHINE_IP`.*

---

## Podrobně

- `-oN` – **normal** (čitelný)
- `-oG` – **grepable** (1 řádek na hostitele, snadné `grep`)
- `-oX` – **XML** (pro zpracování programy)
- `-oA` – všechny tři najednou
- `-oS` – Script Kiddie (leetspeak, nedoporučeno)

**Souvisí:** [[nmap]], [[NSE]], [[detekce služeb]]
