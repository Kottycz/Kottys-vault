---
aliases: [Autorizace, Authorization]
tags: [slovnik]
---

# autorizace

Určení, co smí už ověřený uživatel dělat.

*Příklad: učitel smí soubor jen číst, žák ho smí číst i upravovat.*

---

## Podrobně

Příklad oprávnění k souboru `student.txt`:

| Kdo | Oprávnění |
| :-- | :-- |
| Matyáš | čtení + zápis |
| učitel | čtení |
| ostatní | žádný přístup |

- následuje po [[autentizace|autentizaci]]
- oprávnění se řeší na úrovni uživatele, procesu, souboru a služby
- základ principu nejmenšího privilegia

## Souvisí

[[identifikace|Identifikace]] · [[autentizace|Autentizace]] · [[nejmensi_privilegium|Nejmenší privilegium]] · [[rbac|RBAC]]
