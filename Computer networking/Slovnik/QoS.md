---
aliases: [Quality of Service, kvalita služby]
tags: [slovnik]
---

# QoS

**Quality of Service** – mechanismy, které upřednostňují důležitý provoz před méně důležitým, když je síť vytížená.

---

## Podrobně

### Proč

Když je linka plná, pakety čekají ve frontě nebo se zahazují. Bez QoS se to děje **náhodně** – stahování torrentu může zničit hovor na Teamsech. QoS určí pořadí.

### Co se typicky prioritizuje

```
1. Hlas (VoIP)        ← nejcitlivější na zpoždění a jitter
2. Video, konference
3. Kritické aplikace  (databáze, platby)
4. Web, e-mail
5. Stahování, zálohy  ← může počkat
```

### Parametry, které QoS řeší

| Parametr | Co znamená |
| :-- | :-- |
| **Šířka pásma** | kolik kapacity provoz dostane |
| **[[latency]]** | jak dlouho trvá cesta |
| **Jitter** | kolísání latence |
| **Ztrátovost** | kolik paketů se zahodí |

### Jak to funguje technicky

- **Klasifikace a značkování** – pakety se označí podle typu (pole DSCP v IP hlavičce, CoS u Ethernetu)
- **Fronty** – každá třída má vlastní frontu, důležité se obsluhují dřív
- **Policing / shaping** – omezení nebo vyhlazení rychlosti provozu
- **Zahazování** – při přeplnění se zahodí nejdřív nedůležité pakety

### Kde se s tím setkáš

Firemní sítě, sítě poskytovatelů, domácí routery (často "Smart QoS" nebo "prioritizace zařízení"). QoS ale **nezvýší kapacitu linky** – jen spravedlivěji rozdělí to, co je k dispozici.

### Doporučené hodnoty pro hlas

| Parametr | Pro kvalitní hovor |
| :-- | :-- |
| [[latency|zpoždění]] jednosměrně | do 150 ms |
| jitter | do 30 ms |
| ztráta paketů | do 1 % |

Video a hlas jsou citlivé na zpoždění, e-mail nebo stahování souborů ne.

### Fronty

Když je linka plná, pakety čekají ve frontě. QoS rozhoduje, kdo jde dřív:

- **priority queue** – hlas jde vždy první,
- **weighted fair queuing** – každá třída dostane svůj podíl šířky pásma,
- **FIFO** – bez QoS, kdo dřív přijde, ten dřív odejde.

### Označování

Provoz se označí co nejblíž zdroji (IP telefon, přístupový switch) pomocí [[DSCP]] (vrstva 3) nebo CoS (vrstva 2, [[802.1Q]] tag) a další zařízení pak podle značky rozhodují.

**Souvisí:** [[latency]], [[throughput]], [[router]], [[UDP]]
