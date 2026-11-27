---
tags: [slovnik]
---

# anycast

**Komunikace jeden na nejbližšího** – stejnou adresu má více serverů, provoz se doručí tomu, který je z pohledu směrování nejblíž.

---

## Podrobně

### Princip

Několik serverů po světě inzeruje **tutéž IP adresu**. Směrování pak samo pošle uživatele do nejbližšího uzlu:

```
Uživatel v Praze  ──► server Frankfurt   (stejná IP)
Uživatel v Tokiu  ──► server Singapur    (stejná IP)
```

Uživatel nic nepozná – používá jednu adresu, ale obslouží ho jiný stroj podle polohy.

### K čemu je to dobré

- **Nižší [[latency|latence]]** – odpovídá geograficky bližší server
- **Rozložení zátěže** – provoz se rozdělí mezi uzly
- **Odolnost** – když uzel vypadne, směrování automaticky pošle provoz jinam
- **Obrana proti DDoS** – útok se rozprostře mezi mnoho lokalit

### Kde se používá

- **[[DNS]] root servery** (např. `8.8.8.8` od Googlu)
- **CDN** (Cloudflare, Akamai) – doručování webového obsahu
- Velké cloudové služby

### Podpora

- **[[IPv6]]** – anycast je součástí standardu
- **[[IPv4]]** – realizuje se na úrovni směrování (BGP), formálně není zvláštním typem adresy

### Srovnání

| Typ | Doručí se |
| :-- | :-- |
| [[unicast]] | jednomu konkrétnímu |
| [[broadcast]] | všem v síti |
| [[multicast]] | přihlášené skupině |
| **anycast** | nejbližšímu z několika stejných |

### Příklad: kořenové DNS servery

Kořenových [[DNS]] serverů je 13 jmen (A až M), ale fyzicky jich běží stovky po celém světě. Každý z těch 13 je anycast adresa, takže dotaz z Prahy skončí na nejbližší instanci v Evropě, ne v USA.

### Anycast v IPv6

- [[IPv6]] má anycast přímo v návrhu, adresa se nijak neliší od [[unicast|unicastu]], jen ji má víc zařízení,
- **subnet-router anycast** – adresa podsítě s nulovým ID rozhraní (např. `2001:db8:acad:1::`). Odpoví na ni kterýkoliv [[router]] v té podsíti.

### Proč pozor u TCP

Anycast vybírá cíl podle směrování. Když se během spojení změní cesta, další pakety můžou dorazit na **jiný server**, který o spojení neví. Proto se anycast hodí hlavně pro krátké dotazy ([[DNS]] přes [[UDP]]) a pro CDN, kde se to řeší chytřeji.

**Souvisí:** [[unicast]], [[multicast]], [[broadcast]], [[IPv6]], [[DNS]], [[latency]]
