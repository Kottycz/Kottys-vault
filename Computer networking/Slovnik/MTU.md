---
aliases: [Maximum Transmission Unit]
tags: [slovnik]
---

# MTU

**Maximum Transmission Unit** – největší velikost paketu, který lze poslat po dané lince bez rozdělení. U Ethernetu standardně **1500 bajtů**.

---

## Podrobně

### Co se do MTU počítá

MTU je velikost **užitečného obsahu rámce** – tedy IP paketu včetně jeho hlavičky, ale bez ethernetové hlavičky:

```
[Ethernet hl. 14 B][ IP paket = max 1500 B ][FCS 4 B]
                    └ IP hl. 20 B + TCP hl. 20 B + data 1460 B ┘
```

Těch 1460 B užitečných dat je [[MSS]].

### Typické hodnoty

| Technologie | MTU |
| :-- | :-- |
| Ethernet | 1500 B |
| PPPoE ([[DSL]]) | 1492 B |
| [[VPN]] tunely | 1400–1450 B |
| Jumbo rámce | 9000 B |
| Wi-Fi | 2304 B |

### Fragmentace

Když je paket větší než MTU linky:

- **[[IPv4]]** – [[router]] paket rozdělí na fragmenty (pokud není nastaven příznak DF). Fragmentace je pomalá a když se ztratí jeden fragment, musí se poslat všechno znovu.
- **[[IPv6]]** – routery fragmentovat **nesmí**. Odesílatel musí zjistit nejmenší MTU po cestě (Path MTU Discovery) a rovnou posílat menší pakety.

### Path MTU Discovery

Odesílatel pošle paket s příznakem DF (nefragmentovat). Když narazí na linku s menším MTU, dostane [[ICMP]] zprávu „potřeba fragmentace" s hodnotou MTU a příště pošle menší paket.

Když někdo blokuje ICMP, tohle přestane fungovat → vzniká **black hole**: malé pakety projdou, velké se ztratí (typicky se stránky načítají napůl).

### Jumbo rámce

MTU 9000 B v datových centrech – míň režie na stejný objem dat, ale musí to podporovat **všechna** zařízení po cestě.

**Souvisí:** [[MSS]], [[PDU]], [[zapouzdření]], [[ICMP]], [[goodput]], [[FCS]]
