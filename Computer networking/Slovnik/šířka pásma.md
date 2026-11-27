---
aliases: [bandwidth, šířka pásma]
tags: [slovnik]
---

# šířka pásma

**Teoretická maximální kapacita linky** – kolik dat po ní může projít za sekundu. Udává se v bit/s (Mb/s, Gb/s). Anglicky **bandwidth**.

---

## Podrobně

### Tři pojmy, které se pletou

| Pojem | Co znamená |
| :-- | :-- |
| **Šířka pásma** | co linka **slibuje** (gigabitový port = 1000 Mb/s) |
| **[[throughput]]** | co skutečně naměříš |
| **[[goodput]]** | kolik z toho jsou tvoje užitečná data |

```
Šířka pásma  1000 Mb/s
Throughput    940 Mb/s   ← režie protokolů, sdílení, chyby
Goodput       880 Mb/s   ← bez hlaviček a retransmisí
```

### Bity vs. bajty

| Zkratka | Jednotka | Kde se používá |
| :-- | :-- | :-- |
| **b** | bit | rychlost linky (Mb/s) |
| **B** | bajt | velikost souboru, rychlost stahování (MB/s) |

1 B = 8 b, takže **100 Mb/s ≈ 12,5 MB/s**. Proto se zdá, že stahování jede "osmkrát pomaleji" – ve skutečnosti jde jen o jiné jednotky.

### Typické rychlosti

| Technologie | Šířka pásma |
| :-- | :-- |
| Fast Ethernet | 100 Mb/s |
| Gigabit Ethernet | 1 Gb/s |
| 10G Ethernet | 10 Gb/s |
| Wi-Fi 6 | až 9,6 Gb/s (teoreticky) |

### Co šířku pásma omezuje

Celková rychlost spojení je dána **nejpomalejším úsekem** cesty. Gigabitová síť doma nepomůže, když má připojení od [[ISP|poskytovatele]] 50 Mb/s.

### Převody jednotek

| Jednotka | Hodnota |
| :-- | :-- |
| 1 kb/s | 1 000 b/s |
| 1 Mb/s | 1 000 000 b/s |
| 1 Gb/s | 1 000 000 000 b/s |

Pozor: v sítích se násobí **1000**, ne 1024.

### Příklad výpočtu

Soubor 1 GB (= 8 Gb) přes linku 100 Mb/s: 8 000 Mb / 100 Mb/s = **80 sekund** v ideálním případě. Reálně déle, protože [[throughput]] a [[goodput]] jsou nižší než šířka pásma.

### Šířka pásma na Cisco

`show interfaces` ukazuje u rozhraní `BW 1000000 Kbit/sec`. Tuhle hodnotu používají směrovací protokoly ([[OSPF]], [[EIGRP]]) k výpočtu metriky. Příkaz `bandwidth` ji mění jen pro výpočty, skutečnou rychlost linky nezmění.

**Souvisí:** [[throughput]], [[goodput]], [[latency]], [[QoS]], [[optické vlákno]]
