---
aliases: [Access Control List, seznam oprávnění]
tags: [slovnik]
---

# ACL

**Access Control List** – seznam oprávnění u souboru, složky nebo objektu: kdo smí co. Např. složka `Informatika`: `DL_Informatika_Zapis` = Modify.

---

## Podrobně

- každý záznam (ACE) = účet nebo skupina + povolení/zákaz + právo (Read, Modify, Full Control…)
- oprávnění se vážou na [[SID]], ne na jméno
- dobrá praxe: do ACL dávat jen skupiny, podle [[AGDLP]] jen `DL_` skupiny

**Souvisí:** [[AGDLP]], [[04b_Skupiny_a_AGDLP]]
