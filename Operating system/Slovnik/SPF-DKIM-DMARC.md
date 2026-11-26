---
aliases: [SPF, DKIM, DMARC]
tags: [slovnik]
---

# SPF-DKIM-DMARC

Tři ochrany pošty uložené v [[DNS]] jako **[[DNS záznam|TXT]]** záznamy. Říkají, kdo smí za doménu posílat e-maily a jak ověřit, že zpráva není podvržená.

---

## Podrobně

- **SPF** – seznam serverů, které smí posílat poštu za doménu
- **DKIM** – digitální podpis zprávy, veřejný klíč v [[DNS]]
- **DMARC** – co dělat se zprávou, která SPF/DKIM nesplní (propustit, karanténa, zahodit)

**Souvisí:** [[DNS záznam]], [[03a_DNS_obecne]]
