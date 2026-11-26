---
aliases: [Organizational Unit, organizační jednotka]
tags: [slovnik]
---

# OU

**Organizational Unit** – složka v doméně, do které se třídí uživatelé, počítače a skupiny a na kterou jde navázat [[GPO]]. Např. `Skola\Studenti\Informatika`.

---

## Podrobně

- 3 úlohy: třídění, navázání [[GPO]], delegování správy
- × **kontejner** (`Users`, `Computers`) – [[GPO]] nejde
- `Domain Controllers` je OU
- objekt je jen v jedné OU, ale v mnoha skupinách
- ochrana proti smazání: *Protect container from accidental deletion*

**Souvisí:** [[GPO]], [[AGDLP]], [[04a_Navrh_OU]]
