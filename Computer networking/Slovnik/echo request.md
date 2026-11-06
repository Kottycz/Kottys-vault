---
aliases: [echo reply, ICMP typ 8, ICMP typ 0, Echo Request, Echo Reply]
tags: [slovnik]
---

# echo request

**Zpráva [[ICMP]] typu 8, kterou [[ping]] posílá cíli** s otázkou "jsi tam?". Cíl odpoví zprávou **echo reply** (ICMP typ 0).

---

## Podrobně

### Dvojice zpráv

| Zpráva | ICMP typ | Kdo ji posílá |
| :-- | :-- | :-- |
| **echo request** | **8** | zdroj (ten, kdo pinguje) |
| **echo reply** | **0** | cíl (odpověď) |

### Jak to funguje

```
PC1  ──► echo request (typ 8) ──►  PC2
PC1  ◄── echo reply   (typ 0) ◄──  PC2
```

Podle toho, jestli odpověď dorazí a za jak dlouho, ping zjistí dostupnost a [[latency|odezvu]].

### Proč je to důležité

Ping je **nejúčinnější způsob**, jak rychle otestovat konektivitu **vrstvy 3** mezi zdrojovou a cílovou IP adresou – a opírá se právě o tuhle dvojici zpráv.

### Když odpověď nepřijde

Neznamená to nutně, že zařízení nefunguje – cíl může echo request blokovat ([[firewall]]).

**Souvisí:** [[ICMP]], [[ping]], [[rozšířený ping]], [[latency]], [[firewall]]
