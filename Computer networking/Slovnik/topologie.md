---
aliases: [topologie sítě, mesh, bus, ring, hvězda, star]
tags: [slovnik]
---

# topologie

**Způsob, jakým jsou zařízení v síti propojena.** Rozlišuje se topologie **fyzická** (jak vedou kabely) a **logická** (jak data reálně tečou).

---

## Podrobně

### Topologie LAN

| Topologie | Popis | Stav |
| :-- | :-- | :-- |
| **Sběrnice (bus)** | všichni na jednom sdíleném kabelu | historická (koaxiál) |
| **Kruh (ring)** | zařízení propojená do kruhu | historická (Token Ring) |
| **Hvězda (star)** | všichni do centrálního [[switch\|switche]] | **dnešní standard** |
| **Rozšířená hvězda** | víc propojených hvězd | velké sítě, patra budovy |

### Topologie WAN

| Topologie | Popis |
| :-- | :-- |
| **Point-to-point** | přímé spojení dvou lokalit |
| **Hub and spoke** | centrála a pobočky napojené na ni (jako paprsky kola) |
| **Mesh (mřížka)** | každý s každým – vysoká redundance, ale drahé |
| **Částečný mesh** | kompromis – klíčové uzly propojené víc cestami |

### Fyzická vs. logická topologie

Nejsou totéž. Klasický Ethernet s hubem byl **fyzicky hvězda**, ale **logicky sběrnice** – všichni sdíleli médium a vznikaly kolize. Dnešní [[switch]] je hvězda i fyzicky i logicky.

### Redundance

Víc cest k cíli znamená, že při výpadku jedné se provoz přesměruje jinudy. U [[switch|switchů]] ale redundantní cesty vytvářejí smyčky – proto je potřeba [[STP protokol]].

**Souvisí:** [[LAN]], [[WAN]], [[switch]], [[router]], [[STP protokol]]
