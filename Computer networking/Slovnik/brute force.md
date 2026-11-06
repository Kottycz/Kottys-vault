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

**Souvisí:** [[sniffer]], [[MITM]]
