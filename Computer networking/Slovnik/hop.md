---
aliases: [hopy, hopů, uzel na cestě]
tags: [slovnik]
---

# hop

**Jeden skok na cestě paketu sítí** – každé zařízení vrstvy 3 (obvykle [[router]]), přes které paket projde, je jeden hop.

---

## Podrobně

### Hop a TTL

Každý router paketu sníží [[TTL]] o 1. Číslo, které zbývá, tedy říká, kolik hopů paket ještě smí projít, než se zahodí.

### Hop v traceroute

[[traceroute]] vrací **seznam uzlů (hopů)** při směrování paketu sítí:

```
  1    <1 ms   192.168.1.1     ← 1. hop (domácí router)
  2     8 ms   10.0.0.1        ← 2. hop (poskytovatel)
  3    12 ms   ...             ← 3. hop
```

Díky tomu se dá najít **bod na cestě, kde se problém nachází** – ten hop, kde odezva skočí nahoru nebo kde cesta končí.

### Počet hopů

Čím víc hopů, tím delší trasa. Počet hopů se používá i jako **metrika** u některých směrovacích protokolů (kratší cesta = méně hopů).

**Souvisí:** [[traceroute]], [[TTL]], [[router]], [[ping]]
