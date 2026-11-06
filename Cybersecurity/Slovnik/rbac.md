---
aliases: [RBAC, Role-Based Access Control]
tags: [slovnik]
---

# RBAC (Role-Based Access Control)

Přístupová práva se přidělují podle role, ne konkrétnímu uživateli.

*Příklad: lékař vidí zdravotní dokumentaci, administrativa jen fakturaci.*

---

## Podrobně

Řetězec: **uživatel → role → oprávnění → zdroj**.

| Role | Oprávnění (nemocnice) |
| :-- | :-- |
| lékař | zdravotní dokumentace, výsledky vyšetření |
| sestra | potřebné údaje pacienta, ošetřovatelské informace |
| administrativa | objednávky, fakturace, administrativní údaje |

- politika zůstává stabilní i při personálních změnách
- jednodušší správa a konzistentní pravidla
- podporuje princip nejmenšího privilegia

## Souvisí

[[nejmensi_privilegium|Nejmenší privilegium]] · [[iam|IAM]] · [[autorizace|Autorizace]] · [[pam|PAM]]
