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

### Ostatní LED

| LED | Význam |
| :-- | :-- |
| **SYST** (System) | zelená = funguje, oranžová = chyba |
| **RPS** | záložní zdroj ([[RPS]]) – vypnutá = není připojen, zelená = připojen a připraven |
| **PoE** | stav napájení přes [[PoE]] na portech |

### Tlačítko Mode

Na předním panelu je tlačítko **Mode**. Postupně přepíná, co LED portů ukazují (režimy STAT, DUPLX, SPEED a u PoE switchů i PoE). Podržené tlačítko při zapnutí switche spustí [[boot loader]].

### Barvy STAT LED portu

| Barva | Význam |
| :-- | :-- |
| nesvítí | nic není připojeno nebo je port administrativně vypnutý |
| zelená | link je nahoře |
| bliká zelená | probíhá přenos dat |
| střídá zelená a oranžová | chyby na lince |
| oranžová | port blokuje [[STP protokol|STP]] a nepřeposílá data |

**Souvisí:** [[SYST]], [[RPS]], [[PoE]], [[duplex]], [[switch]], [[POST]]
