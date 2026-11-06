---
aliases: [Cyclic Redundancy Check, cyklický redundantní součet]
tags: [slovnik]
---

# CRC

**Cyclic Redundancy Check** – matematický kontrolní součet, kterým se ověřuje, jestli se data cestou nepoškodila. U Ethernetu se jeho výsledek ukládá do pole [[FCS]].

---

## Podrobně

### Jak funguje

```
Odesílatel:  data → výpočet CRC → připojí výsledek k rámci
Příjemce:    data → výpočet CRC → porovná s připojenou hodnotou

Shoda     → rámec je v pořádku
Neshoda   → rámec je poškozený → ZAHODÍ se
```

Matematicky jde o dělení dat generujícím polynomem – zbytek po dělení je kontrolní součet.

### Jen detekce, ne oprava

CRC pozná, že je něco špatně, ale **neumí to opravit**. Vadný rámec se zahodí a o nápravu se stará až [[TCP]] (vyžádá si data znovu). U [[UDP]] se data prostě ztratí.

### Varianty

| Varianta | Použití |
| :-- | :-- |
| **CRC-32** | Ethernet ([[FCS]]), ZIP, PNG |
| CRC-16 | průmyslové protokoly (Modbus) |
| CRC-8 | jednoduchá zařízení |

### CRC vs. hash

| | CRC | Kryptografický hash (SHA) |
| :-- | :-- | :-- |
| Účel | detekce **náhodných** chyb | ochrana před **úmyslnou** změnou |
| Rychlost | velmi rychlý | pomalejší |
| Bezpečnost | žádná – jde snadno podvrhnout | vysoká |

CRC chrání před šumem na lince, ne před útočníkem.

### Kde se s tím setkáš

Vysoký počet CRC chyb na portu (`show interfaces`) znamená problém s kabelem, konektorem, rušením nebo duplexem.

**Souvisí:** [[FCS]], [[zapouzdření]], [[NIC]], [[switch]], [[UTP]]
