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

### Doporučené konvence

- **brána** = první použitelná adresa (`.1`),
- **síťová zařízení** (switche, AP) = nízké adresy hned za bránou,
- **servery a tiskárny** = statické adresy z vyhrazeného bloku,
- **DHCP pro uživatele** = zbytek rozsahu, statické adresy vyloučit (`ip dhcp excluded-address`),
- vše zapsat do dokumentace (tabulka: zařízení – rozhraní – IP – maska – brána).

### Tabulka adresování (jak ji píšou v labech)

| Zařízení | Rozhraní | IP adresa | Maska | Brána |
| :-- | :-- | :-- | :-- | :-- |
| R1 | G0/0/0 | 192.168.1.1 | 255.255.255.0 | — |
| S1 | VLAN 1 | 192.168.1.2 | 255.255.255.0 | 192.168.1.1 |
| PC-A | NIC | 192.168.1.10 | 255.255.255.0 | 192.168.1.1 |

### Plánování podsítí

U víc podsítí se adresní prostor rozdělí pomocí [[VLSM]] od největší podsítě po nejmenší. Viz [[Subnetting]].

**Souvisí:** [[IP adresa]], [[IPv4]], [[maska podsítě]], [[DHCP]], [[škálování sítě]], [[Budovani_male_site]]
