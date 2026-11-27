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

### Hop a metrika směrování

Některé směrovací protokoly vybírají cestu podle počtu hopů:

- **RIP** – metrika = počet hopů, maximum **15**, 16 = nedosažitelné. Proto se nehodí do velkých sítí,
- [[OSPF]] a [[EIGRP]] počet hopů nepoužívají, rozhoduje šířka pásma, takže zvolí delší cestu přes rychlé linky.

### Next hop

V [[směrovací tabulka|směrovací tabulce]] je u každé cesty **next hop** – IP adresa dalšího routeru, kterému se paket pošle. Router zná jen další krok, ne celou cestu.

```
S  10.0.0.0/8 [1/0] via 192.168.1.2
                         └─ next hop
```

### Switch hop není

[[switch|Switch]] (vrstva 2) neuberá [[TTL]] a v [[traceroute]] se neobjeví. Hop je jen zařízení vrstvy 3.

**Souvisí:** [[traceroute]], [[TTL]], [[router]], [[ping]]
