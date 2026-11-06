---
aliases: [Organizationally Unique Identifier]
tags: [slovnik]
---

# OUI

**Organizationally Unique Identifier** – prvních 24 bitů [[MAC adresa|MAC adresy]], které identifikují **výrobce** síťové karty. Přiděluje je organizace IEEE.

---

## Podrobně

### Umístění v MAC adrese

```
00:1A:2B : 3C:4D:5E
└─ OUI ─┘  └ výrobcem přidělené ┘
 24 bitů        24 bitů
```

- **OUI** – kdo kartu vyrobil (Intel, Cisco, Apple, Samsung…)
- **Zbytek** – pořadové číslo, které výrobce přiděluje svým kartám tak, aby byla adresa jedinečná

### K čemu je to prakticky

- **Identifikace zařízení v síti** – podle OUI poznáš, jestli je neznámé zařízení tiskárna, mobil nebo switch
- **Bezpečnost** – cizí OUI v podnikové síti může odhalit nepovolené zařízení
- **Ladění** – při analýze provozu ve Wiresharku vidíš rovnou jméno výrobce místo čísel

### Speciální bity

V prvním bajtu OUI mají dva bity zvláštní význam:

| Bit | Význam |
| :-- | :-- |
| **I/G** (nejnižší bit) | 0 = [[unicast]], 1 = [[multicast]] |
| **U/L** (druhý nejnižší) | 0 = globálně unikátní (od výrobce), 1 = lokálně nastavená |

Proto adresy s lokálně přepsanou MAC (spoofing) mají nastavený U/L bit.

### Vyhledávání

Databáze OUI je veřejná – existují online vyhledávače, kde po zadání MAC adresy zjistíš výrobce.

### Souvislost s EUI-64

[[EUI-64]] u [[IPv6]] bere MAC adresu, vloží doprostřed `FFFE` a překlopí U/L bit – z OUI se tak stane součást ID rozhraní.

**Souvisí:** [[MAC adresa]], [[NIC]], [[EUI-64]], [[unicast]], [[multicast]]
