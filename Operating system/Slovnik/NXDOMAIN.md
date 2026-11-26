---
aliases: [Non-existent domain, SERVFAIL]
tags: [slovnik]
---

# NXDOMAIN

Odpověď [[DNS]] **„takové jméno neexistuje“** (v nslookup *Non-existent domain*). Např. překlep v jménu nebo chybí záznam.

---

## Podrobně

- **SERVFAIL** – server odpověď nezjistil (chyba konfigurace, nedostupný nadřazený server, [[DNSSEC]])
- **[[DNS]] request timed out** – server neodpovídá (neběží, port 53, špatná [[IP adresa|IP]])
- NXDOMAIN se taky cachuje → nově založené jméno chvíli „není vidět“

**Souvisí:** [[nslookup]], [[03a_DNS_obecne]]
