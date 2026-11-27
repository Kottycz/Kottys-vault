---
aliases: [Start Frame Delimiter, preambule]
tags: [slovnik]
---

# SFD

**Start Frame Delimiter** – 1bajtová značka na začátku ethernetového rámce, která oznamuje "od teď začínají skutečná data". Navazuje na 7bajtovou **preambuli**.

---

## Podrobně

### Umístění v rámci

```
[Preambule][SFD][Cíl MAC][Zdroj MAC][Typ][Data][FCS]
    7 B     1 B    6 B       6 B     2 B         4 B
    └── 8 B synchronizace ──┘
```

### K čemu slouží

- **Preambule** (7 B) – střídání jedniček a nul (`10101010...`), podle kterého si přijímací zařízení **sesynchronizuje hodiny** s odesílatelem
- **SFD** (1 B, `10101011`) – poslední dvě jedničky signalizují konec synchronizace a začátek rámce

Bez synchronizace by příjemce nevěděl, kde přesně jeden bit končí a druhý začíná.

### Proč se nepočítá do velikosti rámce

Preambule ani SFD nejsou součástí rámce jako takového – jsou to jen pomocné signály fyzické vrstvy. Proto se nezapočítávají do [[MTU]] ani do minimální velikosti rámce (64 B).

### Minimální velikost rámce

Rámec musí mít **aspoň 64 bajtů** (bez preambule). Kratší data se doplní **výplní (padding)**. Důvod je historický – souvisí s [[CSMA-CD]]: rámec musel být dost dlouhý, aby odesílatel stihl zaznamenat kolizi dřív, než dovysílá.

Rámce kratší než 64 B se nazývají **runts** a zahazují se jako vadné.

### Preambule + SFD v bitech

```
Preambule: 10101010 10101010 ... (7 bajtů)
SFD:       10101011              (1 bajt)
```

Preambule je střídání 1 a 0, podle kterého si přijímač **synchronizuje hodiny**. SFD končí dvěma jedničkami `11` – tím přijímač pozná, že preambule skončila a hned za ní začíná cílová MAC adresa.

### Ve Wiresharku

Preambuli a SFD Wireshark **neukazuje**, síťová karta je odstraní dřív, než rámec předá systému. Wireshark proto začíná rovnou cílovou MAC adresou.

**Souvisí:** [[FCS]], [[MAC podvrstva]], [[zapouzdření]], [[CSMA-CD]], [[MTU]]
