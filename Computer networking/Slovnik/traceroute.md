---
aliases: [tracert]
tags: [slovnik]
---

# traceroute

**Diagnostický nástroj**, který vypíše všechny [[router|routery]] po cestě k cíli. Využívá postupné zvyšování [[TTL]]. Na Windows `tracert`, na Linuxu `traceroute`.

---

## Podrobně

### Jak funguje

Trik je v [[TTL]] – každý router ho sníží o 1 a při nule paket zahodí a pošle zpět [[ICMP]] Time Exceeded:

```
TTL = 1  →  1. router ho zahodí a ohlásí se  →  známe 1. hop
TTL = 2  →  2. router ho zahodí a ohlásí se  →  známe 2. hop
TTL = 3  →  3. router ...                     →  známe 3. hop
...až dorazí k cíli, který odpoví normálně
```

### Výstup

```
tracert seznam.cz

  1    <1 ms    <1 ms    <1 ms   192.168.1.1
  2     8 ms     7 ms     8 ms   10.0.0.1
  3    12 ms    11 ms    12 ms   ...
  4     *        *        *      Vypršel časový limit požadavku
  5    15 ms    14 ms    15 ms   77.75.79.222
```

Tři časy = tři měření pro každý hop (kvůli přesnosti).

### Co znamenají hvězdičky

`* * *` neznamená přerušenou cestu – ten router jen **neodpovídá na ICMP** (blokuje ho firewall). Pokud se trasa dál normálně pokračuje, je všechno v pořádku. Problém je, až když hvězdičky pokračují do konce.

### K čemu je to prakticky

- Zjistit, **kde** se provoz zasekává (který hop má vysokou odezvu)
- Ověřit, jakou cestou provoz jde (přes kterého poskytovatele)
- Odhalit směrovací smyčku (stejné adresy se opakují dokola)

### ping vs. traceroute

- **[[ping]]** – *je cíl dostupný?* (jen výsledek)
- **traceroute** – *kudy k němu vede cesta a kde vázne?* (celá trasa)

**Souvisí:** [[ping]], [[TTL]], [[ICMP]], [[router]], [[latency]], [[hop]]
