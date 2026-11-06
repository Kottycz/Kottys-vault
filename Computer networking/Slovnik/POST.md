---
aliases: [Power-On Self Test]
tags: [slovnik]
---

# POST

**Power-On Self Test** – automatický **test hardwaru po zapnutí**. Příklad: po zapnutí switche zablikají LED, a když POST selže, [[IOS]] se vůbec nenačte.

---

## Podrobně

- Spouští se jako první krok startu, ještě před [[boot loader|boot loaderem]].
- Kontroluje CPU, paměť a základní komponenty.
- U switche je výsledek vidět na LED: [[SYST]] zelená = OK, **oranžová** = zařízení má napájení, ale něco nefunguje správně.
- Obdoba POST u PC (BIOS píp).

### Pořadí startu switche

1. **POST**
2. [[boot loader]]
3. inicializace CPU
4. inicializace [[flash]]
5. načtení [[IOS]]

**Souvisí:** [[boot loader]], [[IOS]], [[flash]], [[switch]]
