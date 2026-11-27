---
aliases: [latence, zpoždění, RTT]
tags: [slovnik]
---

# latency

**Latence (zpoždění)** – doba, za kterou data doputují ze zdroje do cíle. Měří se v milisekundách. **RTT** je doba cesty tam i zpět.

---

## Podrobně

### Z čeho se skládá

| Složka | Popis |
| :-- | :-- |
| **Propagační** | čas, než signál urazí vzdálenost (limit = rychlost světla) |
| **Serializační** | čas na vyslání všech bitů rámce na linku |
| **Zpracování** | čas, který stráví paket v [[router|routeru]] |
| **Ve frontě** | čekání v bufferu, když je linka vytížená |

### Latence vs. rychlost

To se hodně plete:

| | Co to je | Analogie |
| :-- | :-- | :-- |
| **Latence** | jak dlouho trvá cesta | jak dlouho jede kamion |
| **[[throughput]]** | kolik dat projde za sekundu | kolik toho kamion uveze |

Můžeš mít gigabitovou linku s hroznou latencí (satelit) i pomalou linku s výbornou latencí (lokální síť).

### Typické hodnoty

| Spojení | RTT |
| :-- | :-- |
| Lokální [[LAN]] | < 1 ms |
| Ke známému webu v ČR | 5–20 ms |
| Přes oceán | 100–200 ms |
| Satelit (geostacionární) | 500–600 ms |

### Kde latence vadí

- **Online hry** – vysoký "ping" = zpožděné reakce
- **VoIP a videohovory** – nad ~150 ms je hovor nepříjemný
- **Vzdálené ovládání** (SSH, RDP) – znát zpoždění při psaní

U streamování videa naopak latence tolik nevadí – buffer ji schová.

### Jitter

**Kolísání latence** – když jednou přijde paket za 20 ms a podruhé za 80 ms. U hovorů a her vadí víc než vyšší, ale stabilní latence. Řeší se [[QoS]].

### Jak latenci změřit

- [[ping]] ukáže **RTT** (cesta tam a zpátky) v ms,
- [[traceroute]] ukáže latenci k jednotlivým routerům na cestě, takže vidíš, kde roste.

```
C:\> ping 8.8.8.8
Reply from 8.8.8.8: bytes=32 time=14ms TTL=117
```

### Zpoždění na jednotlivých místech

| Druh zpoždění | Kdy roste |
| :-- | :-- |
| šíření (propagation) | velká vzdálenost, satelit |
| serializace | pomalá linka, velký paket |
| zpracování | přetížený router |
| fronta (queuing) | zahlcená linka |

Proti frontám pomáhá [[QoS]], které pošle hlas a video přednostně.

**Souvisí:** [[throughput]], [[goodput]], [[ping]], [[QoS]], [[traceroute]]
