---
aliases: [Sender Policy Framework]
tags: [slovnik]
---

# SPF

**Sender Policy Framework** – DNS záznam domény se seznamem serverů, které za ni smí posílat e-maily.

*Příklad: e-mail od @firma.cz přišel z IP, která v SPF není → podezřelé.*

---

## Podrobně

- kontroluje se v hlavičkách (`Received-SPF: pass/fail`)

**Souvisí:** [[DKIM]], [[DMARC]], [[phishing]]
