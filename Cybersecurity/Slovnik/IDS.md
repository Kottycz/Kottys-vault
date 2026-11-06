---
aliases: [IDS, Intrusion Detection System]
tags: [slovnik]
---

# IDS (Intrusion Detection System)

Systém, který **kontroluje síťový provoz** a hlásí podezřelé vzorce nebo podpisy útoků.

*Příklad: IDS vyvolá poplach při rychlém skenu portů (-T5).*

---

## Podrobně

- kontroluje hlavičky i **obsah dat**
- pouze **detekuje a hlásí** (na rozdíl od [[IPS]], které provoz i blokuje)
- proti němu pomáhá pomalé skenování (`-T0`, `-T1`), [[fragmentace paketů]] nebo [[decoy scan]]

**Souvisí:** [[IPS]], [[firewall]], [[časování skenování]], [[fragmentace paketů]], [[nmap]]
