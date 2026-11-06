---
aliases: [pomalý start, řízení zahlcení, congestion control]
tags: [slovnik]
---

# slow start

**Pomalý start** – algoritmus [[TCP]] pro **řízení zahlcení**. Odesílatel začne opatrně a rychlost zvyšuje, dokud nenarazí na ztráty paketů.

---

## Podrobně

### Proč

Odesílatel nezná kapacitu sítě mezi sebou a příjemcem. Kdyby začal plnou rychlostí, zahltil by routery po cestě a pakety by se zahazovaly. Proto postupně "zkouší", kolik síť unese.

### Jak probíhá

TCP si drží **congestion window (cwnd)** – kolik smí být nepotvrzených dat na cestě:

```
1. Start:      cwnd = 1 segment
2. Každý ACK:  cwnd se zdvojnásobí   (exponenciální růst)
                 1 → 2 → 4 → 8 → 16 ...
3. Po dosažení prahu (ssthresh):
                 cwnd roste jen o 1 za okružní dobu (lineárně)
                 = fáze congestion avoidance
4. Při ztrátě: cwnd se prudce sníží, práh se sníží,
                 začíná se znovu
```

Vznikne typický "pilový" průběh rychlosti.

### Jak se pozná zahlcení

TCP ztrátu paketu (chybějící ACK nebo tři duplicitní ACK) interpretuje jako **přetížení sítě**, ne jako chybu linky. Proto se na nekvalitních bezdrátových spojích výkon TCP propadá – ztráty tam vznikají rušením, ne zahlcením.

### Slow start vs. sliding window

- **[[sliding window]]** – limit dá **příjemce** (kolik zvládne zpracovat)
- **slow start / cwnd** – limit si odvodí **odesílatel** podle stavu sítě

Skutečná rychlost = menší z obou.

**Souvisí:** [[TCP]], [[sliding window]], [[throughput]], [[latency]]
