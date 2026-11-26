---
aliases: [Automatic Private IP Addressing, 169.254]
tags: [slovnik]
---

# APIPA

**Automatic Private [[IP adresa|IP]] Addressing** – adresa `169.254.x.x/16`, kterou si Windows dá sám, když mu [[DHCP]] server neodpoví. Např. PC v učebně má `169.254.12.34` → [[DHCP]] nefunguje.

---

## Podrobně

- adresa se volí náhodně, obsazenost se ověří přes [[ARP]]
- nemá bránu ani [[DNS]] → jen místní síť
- klient dál zkouší [[DHCP]] každých pár minut
- příčiny: [[DHCP]] neběží / není autorizovaný, scope neaktivní / plný, server v jiné síti bez relay

**Souvisí:** [[DHCP scope]], [[02a_DHCP_teorie]]
