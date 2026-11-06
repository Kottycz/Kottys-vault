---
aliases: [bezstavový firewall, stateful firewall]
tags: [slovnik]
---

# Stavový a bezstavový firewall

Dva typy [[firewall|firewallu]].

*Příklad: Null/FIN/Xmas scan projde bezstavovým, ale ne stavovým.*

---

## Podrobně

- **bezstavový** – kontroluje jen jednotlivé pakety (hledá SYN)
- **stavový** – sleduje spojení a zahodí pakety, které k žádnému nepatří
- proto Null, FIN a Xmas fungují jen proti bezstavovému

**Souvisí:** [[firewall]], [[Null scan]], [[FIN scan]], [[Xmas scan]], [[IDS]]
