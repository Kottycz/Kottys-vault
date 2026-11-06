---
aliases: [Differentiated Services Code Point, DiffServ, ToS]
tags: [slovnik]
---

# DSCP

**Differentiated Services Code Point** – 6bitové pole v IP hlavičce, které označuje **prioritu paketu**. Na jeho základě funguje [[QoS]].

---

## Podrobně

### Umístění v hlavičce

Pole **Differentiated Services (DS)** v [[IPv4]] hlavičce má 8 bitů:

```
[  DSCP (6 bitů)  ][ ECN (2 bity) ]
   priorita          oznámení zahlcení
```

Dřív se celé pole jmenovalo **ToS** (Type of Service) – tenhle starší název se pořád objevuje.

### Běžné hodnoty

| Označení | Použití |
| :-- | :-- |
| **EF** (Expedited Forwarding) | hlas / VoIP – nejvyšší priorita |
| **AF41–AF43** | video |
| **AF21–AF23** | důležitá data |
| **CS0 / Default** | běžný provoz, bez priority |

### Jak se to využije

1. Zařízení nebo [[switch]] paket **označkuje** (nastaví DSCP)
2. [[router|Routery]] po cestě podle značky zařadí paket do fronty
3. Při zahlcení se přednostně obslouží pakety s vyšší prioritou, ostatní čekají nebo se zahazují

### Důležité omezení

DSCP je jen **značka** – sama o sobě nic nedělá. Musí ji respektovat všechna zařízení po cestě. Přes internet se značky běžně **přepisují nebo ignorují**, protože poskytovatel nemá důvod upřednostňovat cizí provoz. QoS tedy funguje spolehlivě jen ve vlastní síti.

### ECN

Zbylé 2 bity slouží k **oznámení zahlcení** – router může paket označit "síť je vytížená" místo toho, aby ho zahodil. [[TCP]] pak zpomalí sám od sebe, bez ztráty dat.

**Souvisí:** [[QoS]], [[IPv4]], [[latency]], [[router]], [[TCP]]
