---
aliases: [Network Address Translation, PAT]
tags: [slovnik]
---

# NAT

**Network Address Translation** – překlad síťových adres. Převádí privátní [[IPv4]] adresy z vnitřní sítě na veřejnou adresu, pod kterou vystupují na internetu.

---

## Podrobně

### Proč existuje

IPv4 adres je málo. Poskytovatel dá domácnosti obvykle **jednu veřejnou adresu**, ale doma je deset zařízení. NAT umožní, aby všechna sdílela tu jednu adresu.

### Jak funguje (PAT)

Nejběžnější varianta je **PAT** (Port Address Translation, taky "NAT overload") – rozlišuje spojení podle [[port|portů]]:

```
Vnitřní síť                 Router (NAT)              Internet

192.168.1.10:51000  ──►  93.99.1.5:51000   ──►  93.184.216.34:443
192.168.1.11:49500  ──►  93.99.1.5:49500   ──►  93.184.216.34:443
192.168.1.12:60200  ──►  93.99.1.5:60200   ──►  8.8.8.8:53
```

Router si v **NAT tabulce** pamatuje, který port patří kterému vnitřnímu zařízení, a odpovědi směruje zpátky správně.

### Typy

| Typ | Popis |
| :-- | :-- |
| **Statický NAT** | 1:1 pevný překlad (jedna privátní ↔ jedna veřejná) |
| **Dynamický NAT** | přiděluje z fondu veřejných adres |
| **PAT / overload** | mnoho privátních → jedna veřejná, rozlišeno porty (nejběžnější) |

### Výhody

- Šetří veřejné IPv4 adresy
- Skrývá vnitřní strukturu sítě
- Funguje jako jednoduchá bariéra – zvenku nelze samo od sebe navázat spojení dovnitř

### Nevýhody

- **Porušuje end-to-end princip** – zvenku není vnitřní zařízení přímo dosažitelné (problém pro hry, VoIP, P2P → řeší se port forwardingem nebo UPnP)
- Přidává zpoždění a zátěž routeru
- Komplikuje některé protokoly

### U IPv6

[[IPv6]] má adres dost, takže **NAT se běžně nepoužívá** – každé zařízení může mít vlastní globální adresu ([[GUA]]).

### Pojmy NAT na Cisco

| Pojem | Co to je | Příklad |
| :-- | :-- | :-- |
| **inside local** | privátní adresa PC uvnitř | 192.168.1.10 |
| **inside global** | veřejná adresa, na kterou se PC přeloží | 203.0.113.5 |
| **outside global** | skutečná adresa serveru venku | 142.250.1.1 |
| **outside local** | adresa serveru, jak ji vidí vnitřek (většinou stejná jako outside global) | 142.250.1.1 |

### Konfigurace PAT (overload)

```
R1(config)# access-list 1 permit 192.168.1.0 0.0.0.255
R1(config)# ip nat inside source list 1 interface g0/0/1 overload
R1(config)# interface g0/0/0
R1(config-if)# ip nat inside
R1(config)# interface g0/0/1
R1(config-if)# ip nat outside
```

- ACL určí, které adresy se překládají,
- `overload` = PAT, všichni sdílí jednu veřejnou IP a rozliší se podle [[port|portů]].

### Ověření

`show ip nat translations` (aktuální překlady), `show ip nat statistics`.

### Privátní rozsahy (RFC 1918)

`10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`. Tyhle adresy se v internetu nesměrují, proto potřebují NAT.

**Souvisí:** [[IPv4]], [[IP adresa]], [[port]], [[router]], [[IPv6]]
