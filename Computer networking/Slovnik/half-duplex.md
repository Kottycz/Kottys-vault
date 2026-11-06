---
aliases: [poloduplexní]
tags: [slovnik]
---

# half-duplex

**Poloduplexní přenos** – data můžou téct oběma směry, ale **vždy jen jedním naráz**. Strany se musí střídat.

---

## Podrobně

### Analogie

Vysílačka – jeden mluví, druhý poslouchá, pak se prohodí ("přepínám"). Nikdy oba zároveň.

### Kde se s tím setkáš

- **Wi-Fi** – rádiový kanál je sdílený, zařízení nemůže vysílat a poslouchat zároveň (proto [[CSMA-CA]])
- **Staré huby a koaxiální Ethernet** – všichni sdíleli jedno médium
- Špatně nastavený port na [[switch|switchi]]

### Důsledek: kolize

Když se dvě zařízení netrefí do střídání a začnou vysílat současně, vznikne **kolize** a data se znehodnotí. Proto je v half-duplexu potřeba přístupová metoda ([[CSMA-CD]] na drátě, [[CSMA-CA]] u Wi-Fi).

### Srovnání

| Režim | Směry | Současně | Kolize |
| :-- | :-- | :-- | :-- |
| Simplex | jeden | – | ne |
| **Half-duplex** | oba | ne | ano |
| [[full-duplex]] | oba | ano | ne |

### Duplex mismatch

Když má jedna strana linky full-duplex a druhá half-duplex, síť sice funguje, ale:

- objevují se kolize a chyby (FCS errors, late collisions)
- [[throughput]] spadne na zlomek očekávané rychlosti
- typicky vzniká ručním nastavením duplexu jen na jednom konci

Řešení: nechat autonegotiation zapnutou na obou stranách, nebo nastavit ručně **obě** stejně.

**Souvisí:** [[full-duplex]], [[CSMA-CD]], [[CSMA-CA]], [[switch]]
