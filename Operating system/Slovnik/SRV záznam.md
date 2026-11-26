---
aliases: [SRV, service record]
tags: [slovnik]
---

# SRV záznam

[[DNS]] záznam, který neukazuje na počítač, ale na **službu** (server + port). Např. `_ldap._tcp.dc._msdcs.kotrba.cyberschool.internal` → `srv1-dc`.

---

## Podrobně

- podle něj klient najde **řadič domény** ([[LDAP]], Kerberos)
- zapisuje je služba **[[Netlogon]]** na [[řadič domény|DC]] do složek `_msdcs`, `_sites`, `_tcp`, `_udp`
- ověření: `nslookup -type=SRV _ldap._tcp.dc._msdcs.kotrba.cyberschool.internal`

**Souvisí:** [[DNS záznam]], [[01c_Jmeno_domeny_a_DNS]]
