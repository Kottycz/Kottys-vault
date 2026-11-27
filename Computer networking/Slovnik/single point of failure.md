---
aliases: [SPOF, jednotlivý bod selhání, jednotlivé body selhání]
tags: [slovnik]
---

# single point of failure

**Jednotlivý bod selhání (SPOF)** – část sítě, jejíž výpadek zastaví celou síť nebo její důležitou část.

---

## Podrobně

### Příklady

- jediný [[router]] do internetu – když spadne, nikdo se nedostane ven
- jediný [[switch]], na který jsou připojeni všichni
- jediný kabel mezi dvěma budovami
- jediný [[DHCP]] server

### Jak se bodů selhání zbavit

Každý takový bod se **zdvojí** nebo se připraví záloha – viz [[redundance]]. Při návrhu sítě se vyplatí projít topologii a u každého zařízení se zeptat: *"Co se stane, když tohle přestane fungovat?"*

### Souvislost s topologií

Typická **hvězda** má bod selhání ve středu (centrální switch). Proto se u důležitých sítí hvězda doplňuje o záložní spoje.

### Jak SPOF najít

Projdi cestu provozu od uživatele k serveru nebo do internetu a u každého prvku se zeptej: „Co se stane, když tohle vypadne?" Když odpověď zní „nikdo se nikam nedostane", je to SPOF.

| Prvek | Řešení |
| :-- | :-- |
| jeden switch v jádru | dva switche, propojené redundantně |
| jedna brána | dva routery s HSRP |
| jedno připojení k internetu | dva [[ISP]] |
| jeden napájecí zdroj | druhý zdroj, [[RPS]], UPS |
| jeden server | cluster, zálohy |

### Cena vs. riziko

Odstranit všechny SPOF je drahé. Firma se rozhodne podle toho, kolik ji stojí výpadek. Banka redundanci potřebuje všude, malá kancelář často snese pár hodin bez internetu.

**Souvisí:** [[redundance]], [[topologie]], [[škálování sítě]], [[switch]], [[router]]
