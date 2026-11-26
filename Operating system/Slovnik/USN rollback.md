---
aliases: [USN, Update Sequence Number]
tags: [slovnik]
---

# USN rollback

Stav, kdy se **řadič domény vrátí v čase** (např. snapshotem) a jeho čísla změn (**USN**) nesedí s ostatními řadiči → replikace se rozbije.

---

## Podrobně

- každá změna v [[AD DS|AD]] má pořadové číslo USN, podle něj se replikuje
- starý řadič by „posílal“ data, která ostatní už přepsali
- ochrana *VM-GenerationID*, ale správně: řadič **nezálohovat snapshotem**, zálohovat **System State**

**Souvisí:** [[snapshot]], [[řadič domény]], [[01b_Radice_domeny_a_FSMO]]
