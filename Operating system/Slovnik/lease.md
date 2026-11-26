---
aliases: [DHCP lease, zápůjčka]
tags: [slovnik]
---

# lease

Doba, na kterou [[DHCP]] server **půjčí** klientovi [[IP adresa|IP]] adresu. Např. výchozích 8 dní.

---

## Podrobně

- obnova: **T1 = 50 %** (unicast původnímu serveru), **T2 = 87,5 %** (broadcast komukoli), po vypršení znovu [[DORA]]
- 8 dní → obnova po 4 a 7 dnech
- `ipconfig /release` adresu vrátí, `/renew` vyžádá

**Souvisí:** [[DHCP scope]], [[02a_DHCP_teorie]]
