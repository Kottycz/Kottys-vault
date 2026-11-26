---
aliases: [Key Management Service, MAK, AVMA, aktivace Windows]
tags: [slovnik]
---

# KMS

**Key Management Service** – licenční server ve vlastní síti, u kterého se stroje samy aktivují. Např. ve škole se aktivuje 100 PC bez zadávání klíčů.

---

## Podrobně

- aktivace platí ~**180 dní** a stroj ji obnovuje; když server nevidí, aktivace vyprší
- **MAK** (Multiple Activation Key) – jeden klíč pro víc strojů, ověřuje Microsoft, omezený počet aktivací
- **AVMA** – [[VM]] se aktivují podle licence Datacenter hostitele
- **Retail/OEM** – 1 klíč = 1 stroj
- příkazy: `slmgr.vbs /ipk <klíč>`, `/ato`, stav `/xpr`

**Souvisí:** [[CAL]], [[00a_Virtualizace_edice_aktivace]]
