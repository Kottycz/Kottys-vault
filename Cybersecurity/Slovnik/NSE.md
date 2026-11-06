---
aliases: [Nmap Scripting Engine, -sC, --script]
tags: [slovnik]
---

# NSE (Nmap Scripting Engine)

Interpret skriptů v jazyce [[Lua jazyk|Lua]], kterým [[nmap]] spouští skripty (~600 v `/usr/share/nmap/scripts`).

*Příklad: `nmap -sC MACHINE_IP`.*

---

## Podrobně

- `-sC` = `--script=default`
- `--script "ftp*"` – vzor
- kategorie: auth, broadcast, brute, default, discovery, dos, exploit, external, fuzzer, intrusive, malware, safe, version, vuln
- skripty **brute**, **dos**, **exploit** jsou rizikové
- cizí skripty nespouštěj od autora, kterému nevěříš

**Souvisí:** [[Lua jazyk]], [[nmap]], [[detekce služeb]], [[brute force]], [[DoS-DDoS]]
