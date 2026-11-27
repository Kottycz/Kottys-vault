---
aliases: [brute force, hrubá síla]
tags: [slovnik]
---

# brute force

**Útok hrubou silou** – systematické zkoušení všech možných kombinací hesla (nebo klíče), dokud se nenarazí na tu správnou.

---

## Podrobně

### Jak funguje

Útočník (nebo spíš program) postupně zkouší kombinace znaků, slova ze slovníku, nebo úniky hesel z jiných služeb (**credential stuffing**), dokud se nepřihlásí.

### Obrana

- **Dlouhá a složitá hesla** – exponenciálně prodlužují dobu potřebnou k uhodnutí
- **Omezení počtu pokusů** – např. Cisco IOS příkaz `login block-for # attempts # within #`
- **Vícefaktorové ověření (MFA)** – samo heslo nestačí ani po uhodnutí

### Brute force vs. slovníkový útok

- **brute force** – zkouší úplně všechny kombinace (`aaaa`, `aaab`, …),
- **slovníkový útok** – zkouší jen hesla ze seznamu (běžná slova, uniklá hesla). Je mnohem rychlejší, protože lidé používají předvídatelná hesla.

### Proč záleží na délce hesla

Počet kombinací = (počet znaků v abecedě) ^ (délka hesla):

| Heslo | Kombinací |
| :-- | :-- |
| 8 malých písmen | 26⁸ ≈ 2 × 10¹¹ |
| 8 znaků, všechny tisknutelné znaky | 94⁸ ≈ 6 × 10¹⁵ |
| 12 znaků, všechny znaky | 94¹² ≈ 5 × 10²³ |

Každý znak navíc zvětší počet kombinací mnohonásobně. Délka pomáhá víc než složitost.

### Obrana na Cisco

```
R1(config)# security passwords min-length 10
R1(config)# login block-for 120 attempts 3 within 60
R1(config)# line vty 0 4
R1(config-line)# exec-timeout 5 0
```

`login block-for` – po 3 neúspěšných pokusech během 60 s zablokuje přihlašování na 120 s.

**Souvisí:** [[sniffer]], [[MITM]]
