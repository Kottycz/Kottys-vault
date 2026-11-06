---
aliases: [plán IP adresování, IP schéma, addressing scheme]
tags: [slovnik]
---

# schéma IP adresování

**Předem navržený plán, kdo dostane jakou [[IP adresa|IP adresu]]** – které adresy jsou pro zařízení, které pro servery a které pro běžné počítače.

---

## Podrobně

### Pravidla

- při implementaci sítě se schéma **vytvoří a dodržuje**
- všichni hostitelé a zařízení v síti musí mít **jedinečnou adresu** (dvě zařízení se stejnou adresou = konflikt)

### K čemu je plánování dobré

- z adresy je hned **poznat typ zařízení** (router, server, tiskárna, počítač)
- usnadňuje **řešení problémů** – například když se provoz analyzuje pomocí [[sniffer|analyzátoru protokolů]] a v zachyceném provozu se podle adres rychle zorientuješ
- s plánem se síť snáz **rozšiřuje** ([[škálování sítě]])

### Příklad plánu pro síť 192.168.1.0/24

| Rozsah | Pro koho | Jak se přiděluje |
| :-- | :-- | :-- |
| `.1` – `.10` | síťová zařízení (router, switche) | staticky |
| `.11` – `.50` | servery, tiskárny | staticky |
| `.51` – `.254` | běžné počítače a telefony | dynamicky přes [[DHCP]] |

Konkrétní rozdělení si každá síť vybírá sama – důležité je, aby **existovalo a bylo zdokumentované** (viz dokumentace sítě ve [[škálování sítě|škálování]]).

**Souvisí:** [[IP adresa]], [[IPv4]], [[maska podsítě]], [[DHCP]], [[škálování sítě]], [[Budovani_male_site]]
