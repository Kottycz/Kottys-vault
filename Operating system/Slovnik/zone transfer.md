---
aliases: [přenos zóny, AXFR]
tags: [slovnik]
---

# zone transfer

**Přenos zóny** – zkopírování celé [[DNS]] zóny z primárního serveru na sekundární.

---

## Podrobně

- používá **[[TCP]]** port 53
- sekundární zóna = kopie jen pro čtení získaná přenosem
- povolovat **jen vybraným serverům** – jinak kdokoli získá seznam všech strojů
- [[AD DS|AD]]-integrované zóny ho nepotřebují (replikují se s [[AD DS|AD]])

**Souvisí:** [[DNS záznam]], [[03b_DNS_na_radici]]
