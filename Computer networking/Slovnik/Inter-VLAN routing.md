---
aliases: [směrování mezi VLAN, směrování mezi sítěmi VLAN, inter-VLAN, inter VLAN routing]
tags: [slovnik]
---

# Inter-VLAN routing

**Inter-VLAN routing** – směrování provozu **mezi různými [[VLAN]]**. Bez něj spolu zařízení v různých VLAN nemluví. Příklad: PC z VLAN 10 pošle data na PC ve VLAN 20, rámec projde přes [[router]], který je přesměruje.

---

## Podrobně

- hostitelé v jedné VLAN **nemohou** komunikovat s hostiteli v jiné VLAN, dokud není k dispozici router nebo [[přepínač vrstvy 3]],
- směrování mezi VLAN využívá zařízení **vrstvy 3**,
- tři možnosti: **1)** tradiční (legacy) směrování mezi VLAN, **2)** [[Router-on-a-Stick]], **3)** přepínač vrstvy 3 s [[SVI]],
- bez VLAN by se broadcast šířil všem zařízením a spotřebovával šířku pásma, VLAN to omezí.

### Tři způsoby v porovnání

| | Legacy | [[Router-on-a-Stick]] | [[přepínač vrstvy 3]] |
| :-- | :-- | :-- | :-- |
| fyzických rozhraní routeru | jedno na každou VLAN | jedno pro všechny | žádný router |
| kabely | mnoho | jeden trunk | žádný |
| rychlost | dobrá | omezená jednou linkou | nejvyšší, směruje se v hardwaru |
| škálovatelnost | špatná | do cca 50 VLAN | velmi dobrá |
| typické použití | dnes skoro nikde | malá síť | střední a velké sítě |

### Legacy (tradiční)

Každá VLAN má vlastní fyzický port na routeru, ze switche do routeru vede tolik kabelů, kolik je VLAN. Porty na switchi jsou access. Funguje to, ale při 10 VLAN potřebuješ 10 portů na routeru, což je drahé a nepraktické.

### Co musí být splněno

- každé VLAN odpovídá jiná IP podsíť,
- každé PC má jako [[default gateway|výchozí bránu]] IP adresu rozhraní, [[subinterface|podrozhraní]] nebo [[SVI]] své VLAN,
- mezi switchem a routerem je správně nastavený trunk (u Router-on-a-Stick).

### Nejčastější chyby

Špatná brána na PC, VLAN chybí na switchi, port do routeru není trunk, chybí `no shutdown` na fyzickém rozhraní routeru, překlep v čísle VLAN u `encapsulation dot1q`.

**Souvisí:** [[VLAN]], [[Router-on-a-Stick]], [[přepínač vrstvy 3]], [[SVI]], [[router]], [[subinterface]]
