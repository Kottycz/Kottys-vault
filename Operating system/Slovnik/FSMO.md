---
aliases: [Flexible Single Master Operations, FSMO role, operation master]
tags: [slovnik]
---

# FSMO

**Flexible Single Master Operations** – 5 úloh v Active Directory, které smí v daný moment vykonávat jen **jeden** řadič, aby nevznikly konflikty. Např. schéma AD smí měnit jen *Schema master*.

---

## Podrobně

Většinu změn v AD může dělat kterýkoli [[řadič domény]] (multi-master). Některé operace ale musí mít jediného „šéfa“:

| Role | Úroveň | Úkol |
| :-- | :-- | :-- |
| **Schema master** | les | změny schématu (typy objektů a atributů) |
| **Domain naming master** | les | přidávání a odebírání domén |
| **PDC emulator** | doména | zdroj času, změny hesel, zamykání účtů |
| **RID master** | doména | přiděluje bloky RID → unikátní SID objektů |
| **Infrastructure master** | doména | odkazy na objekty z jiných domén |

- výpis: `netdom query fsmo`
- role jdou přesunout na jiný řadič (transfer), při havárii převzít násilím (seize)

**Souvisí:** [[AD DS]], [[01_AD_DS]]
