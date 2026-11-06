---
aliases: [ICMP tunneling, ICMP tunel]
tags: [slovnik]
---

# ICMP tunelování

Schování jiného provozu (třeba **SSH**) do **payloadu ICMP** paketů (ping).

*Příklad: echo request s 322 B dat, uvnitř `SSH-2.0-OpenSSH_8.9p1`.*

---

## Podrobně

- normální ping má malý payload (~32–64 B)
- znaky: **velký objem** ICMP, **velké pakety**, divný obsah dat
- používá se pro exfiltraci a C2
- útočník může payload nastavit na 64 B, aby nebyl vidět → je potřeba znát normální provoz
- filtr: `data.len > 64 and icmp`

**Souvisí:** [[ICMP]], [[DNS tunelování]], [[Wireshark]]
