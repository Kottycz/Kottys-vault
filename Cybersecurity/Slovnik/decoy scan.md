---
aliases: [-D, návnady]
tags: [slovnik]
---

# Decoy scan (`-D`)

Sken, který vypadá, že přichází z **více IP adres** – skutečná se mezi návnadami ztratí.

*Příklad: `nmap -D 10.10.0.1,10.10.0.2,ME MACHINE_IP`.*

---

## Podrobně

- `ME` = pozice vlastní IP
- `RND` = náhodná IP návnady
- odpovědi chodí i návnadám

**Souvisí:** [[IP spoofing]], [[IDS]], [[skenování portů]], [[nmap]]
