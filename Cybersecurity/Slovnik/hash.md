---
aliases: [hashovací funkce, hash funkce, SHA-1, SHA-256, MD5, bcrypt, hashe]
tags: [slovnik]
---

# hash

Jednosměrná funkce, která z libovolných dat udělá **otisk pevné délky**. Zpátky se data získat nedají.

*Příklad: `sha256("heslo")` = `5e88489…` – stačí změnit jedno písmeno a hash je úplně jiný.*

---

## Podrobně

- použití: kontrola **integrity** souborů, ukládání **hesel**, [[IOC]] (hash malwaru)
- **MD5, SHA-1** – zastaralé, prolomitelné (Adult Friend Finder: 99 % hesel)
- **SHA-256** – bezpečný pro integritu
- **bcrypt** – pomalý schválně, vhodný na hesla

**Souvisí:** [[IOC]], [[cia_triada]]
