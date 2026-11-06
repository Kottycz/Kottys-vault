---
aliases: [-sV, service detection, version detection]
tags: [slovnik]
---

# Detekce služeb (`-sV`)

Zjištění **softwaru a verze** služby na otevřeném portu.

*Příklad: `22/tcp open ssh OpenSSH 6.7p1`.*

---

## Podrobně

- `-sV` dokončí handshake → **nelze stealth**
- `--version-intensity 0–9`, `--version-light` (2), `--version-all` (9)
- zkratka `-A` zahrnuje `-sV`

**Souvisí:** [[detekce OS]], [[NSE]], [[nmap]], [[skenování portů]], [[3-way handshake]]
