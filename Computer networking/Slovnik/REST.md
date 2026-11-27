---
aliases: [Representational State Transfer, REST API]
tags: [slovnik]
---

# REST

**Representational State Transfer** – způsob, jak navrhovat webové služby (API). Používá běžné [[HTTP]] metody a adresy místo vlastního protokolu.

---

## Podrobně

### Princip

Každý zdroj (uživatel, objednávka, produkt) má svoji **URL adresu** a pracuje se s ním pomocí standardních HTTP metod:

| Metoda | Co dělá | Příklad |
| :-- | :-- | :-- |
| **GET** | načti | `GET /uzivatele/5` |
| **POST** | vytvoř | `POST /uzivatele` |
| **PUT** | nahraď | `PUT /uzivatele/5` |
| **DELETE** | smaž | `DELETE /uzivatele/5` |

Odpověď se posílá nejčastěji ve formátu **JSON**.

### Vlastnosti

- **Bezstavové** – server si mezi požadavky nic nepamatuje, každý požadavek nese vše potřebné
- **Jednotné rozhraní** – všechny služby fungují stejným způsobem
- **Nezávislé na jazyce** – klient může být v čemkoliv (JavaScript, Python, mobilní aplikace)

### K čemu se používá

Komunikace mezi aplikacemi: mobilní appka si přes REST API tahá data ze serveru, weby spolu vyměňují informace, cloudové služby nabízejí REST rozhraní ke správě.

### REST není protokol

Je to **architektonický styl** – sada doporučení, jak API postavit. Samotný přenos zajišťuje [[HTTP]] (resp. [[HTTPS]]).

### Formát dat

REST API vrací data nejčastěji ve formátu **JSON**:

```json
{
  "hostname": "R1",
  "interfaces": [
    {"name": "GigabitEthernet0/0/0", "ip": "192.168.1.1", "status": "up"}
  ]
}
```

### HTTP metody a co dělají

| Metoda | Akce | Příklad |
| :-- | :-- | :-- |
| GET | čtení | seznam rozhraní |
| POST | vytvoření | nová VLAN |
| PUT / PATCH | změna | změnit popis rozhraní |
| DELETE | smazání | smazat VLAN |

### REST v sítích

Moderní síťová zařízení a kontroléry (Cisco DNA Center, Meraki) mají REST API. Místo ručního psaní příkazů na každém switchi se konfigurace pošle skriptem (Python) na všechna zařízení najednou. Tomu se říká **automatizace sítě**.

**Souvisí:** [[HTTP]], [[HTTPS]], [[TCP]], [[port]]
