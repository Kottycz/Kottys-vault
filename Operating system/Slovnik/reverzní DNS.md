---
aliases: [reverzní zóna, PTR, in-addr.arpa]
tags: [slovnik]
---

# reverzní DNS

Překlad **[[IP adresa|IP]] adresy na jméno** pomocí záznamů **PTR** v reverzní zóně. Např. `192.168.16.20` → `srv2-fs.kotrba.cyberschool.internal`.

---

## Podrobně

- zóna = síť **pozpátku** + `in-addr.arpa`: `192.168.16.0/24` → `16.168.192.in-addr.arpa`
- záznam PTR se jmenuje posledním číslem adresy (`20`)
- reverzní zóna **nevzniká sama**, záznam A starší než zóna nemá PTR
- nový A s PTR: `-CreatePtr` / *Create associated pointer (PTR) record*
- použití: logy, diagnostika (`ping -a`, `tracert`), pošta

**Souvisí:** [[DNS záznam]], [[03b_DNS_na_radici]]
