---
aliases: [roaming profile, cestovní profil]
tags: [slovnik]
---

# kočovný profil

**Roaming profile** – profil uživatele (plocha, nastavení, `NTUSER.DAT`) se po odhlášení zkopíruje na server a na jiném PC se stáhne zpět. Např. Eva má stejnou plochu na každém PC.

---

## Podrobně

- cesta v [[ADUC]] → Profile → Profile path: `\\SRV1-DC\profiles$\%username%`
- složku (`eva.student.V6`) založí Windows sám při prvním odhlášení
- × **domovská složka** `H:` – sem uživatel ukládá záměrně
- moderní alternativy: FSLogix, Enterprise State Roaming

**Souvisí:** [[04c_Ucty_a_pripojeni_PC]]
