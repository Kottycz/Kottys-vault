---
aliases: [checkpoint]
tags: [slovnik]
---

# snapshot

Uložený stav [[VM|virtuálního stroje]] (disk, případně paměť), ke kterému se jde vrátit. Např. před instalací role.

---

## Podrobně

- **není záloha**: je na stejném hostiteli, řada snapshotů zpomaluje disk, návrat zahodí i dobrou práci
- u řadiče domény hrozí **[[USN rollback]]** → zálohuje se *System State*

**Souvisí:** [[VM]], [[hypervizor]], [[01b_Radice_domeny_a_FSMO]]
