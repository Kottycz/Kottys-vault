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

**Souvisí:** [[HTTP]], [[HTTPS]], [[TCP]], [[port]]
