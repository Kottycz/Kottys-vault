---
aliases: [pevná konfigurace, modulární konfigurace, fixed, modular, pevné zařízení]
tags: [slovnik]
---

# modulární zařízení

**Síťové zařízení s výměnnými moduly** (sloty pro další karty), které se dá rozšiřovat. Opakem je zařízení s **pevnou konfigurací**, kde se porty nedají přidat.

---

## Podrobně

### Dvě fyzické konfigurace

Síťová zařízení ([[switch|switche]], [[router|routery]]) jsou k dispozici v pevné a modulární konfiguraci:

| | Pevná konfigurace | Modulární konfigurace |
| :-- | :-- | :-- |
| Porty a rozhraní | **specifický počet a typ**, nelze rozšiřovat | dají se **přidat moduly** (karty) |
| Cena | levnější | dražší |
| Flexibilita | nízká | vysoká |
| Typické použití | malá síť, kancelář | rostoucí síť, centrální zařízení |

### Proč na tom záleží

Když se v malé síti dojdou porty u pevného switche, musí se koupit další zařízení. Modulární zařízení se dá rozšířit o další kartu a zbytek zůstane.

Zařízení s vyššími rychlostmi a větší rozšiřitelností jsou dražší, ale síť se pak může vyvíjet **bez výměny centrálních zařízení** – viz [[škálování sítě]].

### Další kritéria při výběru

Kromě rozšiřitelnosti se při výběru zařízení pro malou síť sleduje **cena** (podle kapacity a funkcí – počet a typy portů, rychlost propojovací desky) a **rychlost a typy portů/rozhraní**.

### Příklady

- **pevná konfigurace** – běžný switch Catalyst 2960 s 24 nebo 48 porty, nedá se rozšířit,
- **modulární** – šasi Catalyst 9400 nebo 6500, do kterého se zasouvají karty s porty, napájecí zdroje a řídicí moduly,
- **stohovatelné** (stackable) – samostatné switche propojené speciálním kabelem, chovají se jako jeden switch s jednou konfigurací.

### SFP moduly

I switch s pevnou konfigurací má často **SFP sloty** – malé zásuvné moduly, které určí typ portu (optika multimode, singlemode, metalika). Stejný slot tak může mít optický i metalický spoj.

### Výhody a nevýhody

| | Modulární | Pevná konfigurace |
| :-- | :-- | :-- |
| cena na začátku | vysoká | nízká |
| rozšíření | přidáním karty | koupí dalšího switche |
| redundance | dva zdroje, dva řídicí moduly | omezená |
| použití | jádro sítě, datová centra | přístupová vrstva |

**Souvisí:** [[škálování sítě]], [[switch]], [[router]], [[port]], [[Budovani_male_site]]
