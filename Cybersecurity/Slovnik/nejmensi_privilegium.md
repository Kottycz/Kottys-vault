---
aliases: [Nejmenší privilegium, Least privilege]
tags: [slovnik]
---

# nejmenší privilegium

Princip návrhu – uživatel, aplikace nebo proces má jen taková oprávnění, která nutně potřebuje k úkolu. „Potřebuje → dostane, nepotřebuje → nemá.“

*Příklad: student smí psát dokumenty, ale ne měnit systémové soubory.*

---

## Podrobně

- menší útočná plocha a menší dopad incidentu (napadený standardní uživatel škodí méně než napadený admin)
- realizace: RBAC, LUA, sandbox, PAM, JIT (dočasná oprávnění), UAC ve Windows
- nutná průběžná revize a audit oprávnění

## Souvisí

[[rbac|RBAC]] · [[lua|LUA]] · [[sandboxing|Sandboxing]] · [[pam|PAM]] · [[jit|JIT]] · [[uac|UAC]] · [[iam|IAM]] · [[standardni_uzivatel|Standardní uživatel]] · [[administrator|Administrátor]] · [[Principy kybernetické bezpečnosti#Princip nejnižších oprávnění (Least Privilege) – podrobně|Least Privilege podrobně]]
