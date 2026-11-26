---
aliases: [Distinguished Name]
tags: [slovnik]
---

# DN

**Distinguished Name** – úplná cesta k objektu v [[AD DS|AD]]. Např. `CN=Eva Svobodová,OU=Informatika,OU=Studenti,OU=Skola,DC=kotrba,DC=cyberschool,DC=internal`.

---

## Podrobně

- čte se **zprava doleva**: doména → [[OU]] → objekt
- `CN` = jméno objektu, `OU` = organizační jednotka, `DC` = část domény
- používá se v PowerShellu (`-Path`, `-SearchBase`) a ADSI Edit

**Souvisí:** [[UPN]], [[SID]], [[OU]], [[01a_Domena_a_AD]]
