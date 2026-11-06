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

**Souvisí:** [[IPv4]], [[IP adresa]], [[port]], [[router]], [[IPv6]]
