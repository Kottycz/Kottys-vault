---
aliases: [databáze AD]
tags: [slovnik]
---

# NTDS.dit

Soubor s **databází Active Directory** na každém [[řadič domény|řadiči domény]]. Výchozí cesta `C:\Windows\NTDS`.

---

## Podrobně

- obsahuje všechny objekty domény (uživatele, skupiny, počítače, hesla v hashi)
- mezi řadiči se replikuje (multi-master)
- nezálohuje se jako soubor ani snapshotem, ale přes **System State**

**Souvisí:** [[SYSVOL]], [[AD DS]], [[01a_Domena_a_AD]]
