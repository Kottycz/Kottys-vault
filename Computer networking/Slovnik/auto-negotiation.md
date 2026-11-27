---
aliases: [autonegotiation, automatické vyjednávání]
tags: [slovnik]
---

# auto-negotiation

**Auto-negotiation** – porty si po zapojení kabelu **samy domluví** nejlepší společnou **rychlost** a [[duplex]]. Příklad: PC umí 1000 Mb/s full-duplex, starý switch jen 100 Mb/s → domluví se na 100 Mb/s.

---

## Podrobně

### Jak funguje

- Obě strany oznámí, co umí (10 / 100 / 1000 Mb/s, half / full).
- Vyberou se **nejlepší společné** parametry.
- Port při 10/100 Mb/s zvládá [[half-duplex]] i [[full-duplex]], při **1000 Mb/s jen full-duplex**.

### Kdy ho nechat zapnuté

Když nevíš, co je na druhé straně, nebo se zařízení často mění (uživatelské porty).

### Kdy nastavit ručně

U **známých zařízení** (servery, routery, uplinky mezi switchi) je best practice nastavit rychlost i duplex **ručně na obou koncích**.

### Riziko

Když jedna strana běží auto a druhá je pevně nastavená, auto strana nedostane vyjednávání a často zvolí **half-duplex** → [[duplex]] mismatch, [[late collision]] a [[CRC]] chyby. **Selhání auto-negotiation vytváří nesoulad.**

### Souvislost s Auto-MDIX

[[Auto-MDIX]] funguje správně jen když jsou rychlost i duplex nastaveny na **auto**.

### Když druhá strana auto nemá

Když je jeden port na `auto` a druhý ručně (např. 100/full), port s auto pozná **rychlost** podle signálu, ale **duplex nepozná**. U 10/100 Mb/s pak předpokládá **half-duplex** → vznikne nesoulad duplexu (duplex mismatch). Proto platí: buď **auto na obou stranách**, nebo **ručně na obou**.

### Příkazy

```
S1(config-if)# speed auto
S1(config-if)# duplex auto
S1# show interfaces status
```

V `show interfaces status` vidíš u portu např. `a-full a-100`. Písmeno **a-** znamená, že hodnota byla vyjednaná automaticky.

### Gigabit

Pro 1000BASE-T (gigabit po metalice) je auto-negotiation **povinná**, gigabit jede vždy jen full-duplex.

**Souvisí:** [[duplex]], [[Auto-MDIX]], [[full-duplex]], [[half-duplex]], [[Ethernet]]
