---
aliases: [stav portu, stavy portu]
tags: [slovnik]
---

# Stavy portů

Šest stavů, které [[nmap]] přiřazuje portu podle odpovědi.

*Příklad: `22/tcp open ssh`.*

---

## Podrobně

- **open** – služba naslouchá
- **closed** – dostupný, ale nic neposlouchá
- **filtered** – Nmap nepozná, zda je otevřený (blokuje [[firewall]])
- **unfiltered** – dostupný, stav neznámý ([[ACK scan]])
- **open|filtered** – nelze rozlišit (UDP, Null, FIN, Xmas)
- **closed|filtered** – nelze rozlišit (idle scan)

**Souvisí:** [[skenování portů]], [[port]], [[firewall]], [[ACK scan]], [[nmap]]
