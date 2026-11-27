---
tags: [slovnik]
---

# multicast

**Komunikace jeden na skupinu** – data se přenášejí jen zařízením, která se přihlásila k odběru dané skupiny. Šetří kapacitu oproti [[broadcast|broadcastu]].

---

## Podrobně

### Princip

Odesílatel pošle data **jednou**, síť je rozkopíruje jen tam, kde je někdo poslouchá:

```
Zdroj ──► Router ──┬──► PC1 (přihlášen)
                   ├──► PC3 (přihlášen)
                   └──✗  PC2 (nepřihlášen, nic nedostane)
```

Bez multicastu by musel zdroj poslat stejná data zvlášť každému ([[unicast]]) nebo obtěžovat všechny ([[broadcast]]).

### Adresy

| Verze | Rozsah |
| :-- | :-- |
| [[IPv4]] | 224.0.0.0 – 239.255.255.255 |
| [[IPv6]] | ff00::/8 |
| [[MAC adresa]] (IPv4) | začíná `01:00:5E` |
| MAC (IPv6) | začíná `33:33` |

### Známé multicastové adresy

| Adresa | Skupina |
| :-- | :-- |
| 224.0.0.1 | všechna zařízení v segmentu |
| 224.0.0.2 | všechny [[router|routery]] |
| 224.0.0.5 | [[OSPF]] routery |
| ff02::1 | všechna IPv6 zařízení |
| ff02::2 | všechny IPv6 routery |

### Kde se používá

- **IPTV a streamování** živého vysílání
- **Směrovací protokoly** ([[OSPF]], EIGRP) – oznamování mezi routery
- **[[NDP]]** u IPv6 – objevování sousedů
- Videokonference

### Přihlašování ke skupině

Zařízení oznámí zájem protokolem **IGMP** (IPv4) nebo **MLD** (IPv6). Switche umí naslouchat těmto zprávám (IGMP snooping) a posílat multicast jen na relevantní porty.

### Multicast na vrstvě 2

IPv4 multicast adresa se převede na MAC adresu tvaru `01:00:5E:xx:xx:xx` (posledních 23 bitů z IP). Switch bez dalších funkcí posílá multicast **jako broadcast** na všechny porty. Funkce **IGMP snooping** na switchi sleduje, kdo se ke skupině přihlásil, a posílá multicast jen na ty porty.

### IPv6 multicast

[[IPv6]] nemá broadcast, používá jen multicast. Adresy začínají `FF`:

| Adresa | Komu |
| :-- | :-- |
| `FF02::1` | všem zařízením v segmentu (obdoba broadcastu) |
| `FF02::2` | všem routerům v segmentu |
| `FF02::1:FFxx:xxxx` | solicited-node (používá [[NS]] a [[DAD]]) |

### Multicast a směrovací protokoly

| Protokol | Adresa |
| :-- | :-- |
| [[OSPF]] | 224.0.0.5, 224.0.0.6 |
| [[EIGRP]] | 224.0.0.10 |
| RIPv2 | 224.0.0.9 |

Rozsah `224.0.0.0/24` je **link-local**, routery ho nepřeposílají do jiných sítí.

**Souvisí:** [[unicast]], [[broadcast]], [[anycast]], [[IPv6]], [[NDP]], [[OSPF]]
