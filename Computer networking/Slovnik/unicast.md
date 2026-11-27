---
tags: [slovnik]
---

# unicast

**Komunikace jeden na jednoho** – data se přenášejí jedinému konkrétnímu koncovému zařízení. Nejběžnější typ provozu v síti.

---

## Podrobně

### Jak funguje

Rámec/paket má v cílové adrese konkrétní [[MAC adresa|MAC]] nebo [[IP adresa|IP adresu]] jediného příjemce. [[switch|Switch]] ho pošle jen na port, kde ten příjemce je.

```
PC1 ──────► PC3       (PC2 a PC4 nic nedostanou)
```

### Kde se používá

Prakticky všechna běžná komunikace: prohlížení webu ([[HTTP]]), e-mail, stahování souborů, SSH.

### Srovnání typů přenosu

| Typ | Příjemců | Příklad |
| :-- | :-- | :-- |
| **unicast** | jeden | web, e-mail |
| **[[broadcast]]** | všichni v síti | [[ARP]] dotaz, [[DHCP]] Discover |
| **[[multicast]]** | definovaná skupina | IPTV, směrovací protokoly |
| **[[anycast]]** | nejbližší z více serverů | [[DNS]] root servery, CDN |

### U IPv6

[[IPv6]] zná unicast, multicast a anycast – **broadcast v něm neexistuje** (nahradil ho cílený multicast).

### Unicast na vrstvě 2 a 3

| Vrstva | Unicast adresa |
| :-- | :-- |
| 2 | [[MAC adresa]] konkrétní karty, nejnižší bit prvního oktetu = 0 |
| 3 | [[IP adresa]] konkrétního rozhraní |

Paket z PC na server přes internet má po celou cestu **stejnou unicast IP** cíle, ale cílová MAC se na každém routeru mění na MAC dalšího skoku.

### Neznámý unicast

Když switch cílovou MAC nezná, rozešle unicast rámec všem jako broadcast – viz [[neznámý unicast]].

**Souvisí:** [[broadcast]], [[multicast]], [[anycast]], [[MAC adresa]], [[IP adresa]]
