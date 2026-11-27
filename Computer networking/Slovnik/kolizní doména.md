---
aliases: [collision domain]
tags: [slovnik]
---

# kolizní doména

**Kolizní doména** – segment sítě, jehož zařízení sdílejí stejnou šířku pásma, takže při současném vysílání dojde ke [[kolize|kolizi]]. Příklad: všechny počítače na jednom hubu.

---

## Podrobně

- typické pro starší sítě s rozbočovači (huby), kde se zařízení přetahovala o sdílené médium,
- dvě nebo více zařízení vysílá současně → kolize,
- plně duplexní port přepínače kolizní doménu **eliminuje** ([[full-duplex]]),
- [[router]] segmentuje kolizní domény i [[broadcast doména|broadcast domény]].

### Jak spočítat kolizní domény

| Zařízení | Kolizních domén |
| :-- | :-- |
| hub s 8 PC | 1 (všechny porty dohromady) |
| switch s 8 PC | 8 (každý port vlastní) |
| router se 2 porty | 2 |

Příklad: router, na jednom portu switch se 3 PC, na druhém hub se 3 PC. Kolizních domén je: 3 (porty switche k PC) + 1 (spoj switch–router) + 1 (celý hub včetně spoje k routeru) = **5**.

### Velikost kolizní domény

Čím víc zařízení v jedné kolizní doméně, tím častěji se trefí do vysílání naráz a tím víc kolizí. Proto huby nahradily switche.

**Souvisí:** [[kolize]], [[full-duplex]], [[half-duplex]], [[broadcast doména]], [[router]], [[Koncepty_prepinani]]
