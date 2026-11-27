---
aliases: [propustnost]
tags: [slovnik]
---

# throughput

**Propustnost** – množství dat, které skutečně projde linkou za jednotku času (bit/s, Mb/s). Na rozdíl od šířky pásma jde o **reálně naměřenou** hodnotu.

---

## Podrobně

### Tři pojmy, které se pletou

| Pojem | Co znamená |
| :-- | :-- |
| **Bandwidth** (šířka pásma) | teoretické maximum linky (např. "gigabitový port") |
| **Throughput** (propustnost) | co skutečně projde (vždy nižší než bandwidth) |
| **[[goodput]]** | jen užitečná data, bez režie hlaviček a opakování |

```
Bandwidth  1000 Mb/s   ← co linka slibuje
Throughput  940 Mb/s   ← co reálně naměříš
Goodput     880 Mb/s   ← co z toho jsou tvoje data
```

### Proč je throughput nižší než bandwidth

- **Režie protokolů** – hlavičky [[TCP]], IP a Ethernetu zabírají místo
- **Sdílení linky** – kapacitu si dělí víc uživatelů
- **Nejpomalejší úsek** – celková rychlost je dána nejužším místem cesty
- **Retransmise** – ztracená data se posílají znovu
- **[[latency]]** – při vysoké latenci nestíhá TCP zaplnit linku (viz [[sliding window]])
- Zahlcení, chyby, kvalita kabeláže

### Jednotky – pozor na b vs. B

- **b** = bit, **B** = bajt (1 B = 8 b)
- Linky se udávají v **Mb/s**, stahování v prohlížeči v **MB/s**
- 100 Mb/s ≈ 12,5 MB/s

### Jak se měří

Přenosem velkého souboru nebo nástroji jako iperf, speedtest. Výsledek vždy závisí na protokolu, vzdálenosti a vytížení sítě.

### Co throughput snižuje

| Příčina | Proč |
| :-- | :-- |
| režie protokolů | hlavičky, potvrzování ([[goodput]]) |
| [[latency|latence]] | TCP čeká na potvrzení |
| chyby a ztráty | data se posílají znovu |
| sdílené médium | Wi-Fi, half-duplex |
| nejpomalejší linka na cestě | celá cesta je jen tak rychlá jako její nejslabší místo |
| výkon zařízení | přetížený router, pomalý disk serveru |

### Měření

- **iperf3** – změří throughput mezi dvěma PC v síti (`iperf3 -s` na serveru, `iperf3 -c IP` na klientovi),
- speedtest – throughput k internetu,
- `show interfaces` – aktuální provoz na rozhraní (input/output rate).

**Souvisí:** [[goodput]], [[latency]], [[QoS]], [[sliding window]], [[full-duplex]]
