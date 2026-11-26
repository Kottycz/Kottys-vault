---
aliases: [Accounts Global Domain Local Permissions]
tags: [slovnik]
---

# AGDLP

**Accounts → Global groups → Domain Local groups → Permissions** – model přidělování oprávnění přes skupiny. Např. `eva.student` → `GG_Studenti_IT` → `DL_Informatika_Zapis` → Modify na složce.

---

## Podrobně

- **Global** skupina = lidé podle role, **Domain Local** = právo ke zdroji
- oprávnění u zdroje dostane **jen DL skupina**, nikdy člověk
- změna přístupu = změna členství, [[ACL]] zůstává stejné

**Souvisí:** [[ACL]], [[OU]], [[04b_Skupiny_a_AGDLP]]
