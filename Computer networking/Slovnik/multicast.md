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

**Souvisí:** [[unicast]], [[broadcast]], [[anycast]], [[IPv6]], [[NDP]], [[OSPF]]
