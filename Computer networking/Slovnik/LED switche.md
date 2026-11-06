---
aliases: [LED indikátory, kontrolky switche, Mode button]
tags: [slovnik]
---

# LED switche

**LED switche** – kontrolky na předním panelu, podle kterých rychle poznáš **stav switche a portů** (napájení, link, duplex, rychlost, PoE). Příklad: zelená LED u portu = je tam link, blikající zelená = přenáší se data.

---

## Podrobně

U Catalyst 2960 jsou LED 1–6 vlevo, **tlačítko Mode** (7) a LED portů (8). Mode přepíná, co LED portů právě ukazují: **STAT → DUPLX → SPEED → PoE**.

| LED | Co ukazuje |
| :-- | :-- |
| [[SYST]] | napájení a funkce systému |
| [[RPS]] | záložní zdroj |
| **STAT** | stav portů (výchozí režim) |
| **DUPLX** | [[duplex]] portů |
| **SPEED** | rychlost portů |
| [[PoE]] | napájení přes ethernet |

### STAT – LED portu

- vypnuto = není link nebo port je **shutdown**
- **zelená** = link je
- **blikající zelená** = aktivita (odesílá/přijímá)
- **střídavě zelená–oranžová** = chyba linku
- **oranžová** = port blokován (ochrana proti smyčce, ~30 s po aktivaci je to normální)
- **blikající oranžová** = port blokován kvůli možné smyčce

### DUPLX – LED portu

- zelená = [[full-duplex]]
- zhasnutá = [[half-duplex]]

### SPEED – LED portu

- vypnuto = **10 Mb/s**
- zelená = **100 Mb/s**
- blikající zelená = **1000 Mb/s**

**Souvisí:** [[SYST]], [[RPS]], [[PoE]], [[duplex]], [[switch]], [[POST]]
