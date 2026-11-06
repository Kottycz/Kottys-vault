---
aliases: [JIT, Just-in-Time, Just-in-Time přístup]
tags: [slovnik]
---

# JIT (Just-in-Time)

Dočasné oprávnění – uživatel dostane vyšší práva jen na dobu konkrétního úkolu a pak se mu automaticky odeberou.

*Příklad: admin si na hodinu vyžádá práva na úpravu serveru, po hodině je zase nemá.*

---

## Podrobně

Postup:

| Krok | Co se děje |
| :-- | :-- |
| 1. Standardní uživatel | běžná práce s minimem práv |
| 2. Žádost | uživatel potřebuje vyšší oprávnění |
| 3. Ověření | kontrola identity a oprávněnosti žádosti |
| 4. Dočasné oprávnění | práva se přidělí |
| 5. Úkol | práce, která práva vyžaduje |
| 6. Odebrání | práva se automaticky odeberou |

**Výhody:**
- kratší doba privilegovaného přístupu
- menší prostor pro zneužití
- lepší audit
- menší dopad kompromitovaného účtu

Ideální stav: administrátor není administrátorem celý den, ale jen během konkrétního úkolu.

## Souvisí

[[nejmensi_privilegium|Nejmenší privilegium]] · [[pam|PAM]] · [[uac|UAC]] · [[lua|LUA]]
