---
aliases: [Time To Live, Hop Limit]
tags: [slovnik]
---

# TTL

**Time To Live** – čítač v hlavičce IP paketu, který se na každém [[router|routeru]] sníží o 1. Při dosažení nuly se paket zahodí. Chrání síť před nekonečným kolováním paketů.

---

## Podrobně

### Proč existuje

Kdyby se ve směrování objevila smyčka (router A posílá na B, B zpátky na A), paket by kroužil donekonečna a zahltil síť. TTL zaručí, že každý paket má omezenou životnost.

### Jak to probíhá

```
Odesílatel:  TTL = 64
1. router:   TTL = 63
2. router:   TTL = 62
...
n. router:   TTL = 0  →  paket zahozen
             →  zpět odesílateli jde [[ICMP]] Time Exceeded
```

### Typické počáteční hodnoty

| Systém | Výchozí TTL |
| :-- | :-- |
| Linux / macOS | 64 |
| Windows | 128 |
| Síťová zařízení (Cisco) | 255 |

Z TTL v odpovědi na [[ping]] se dá odhadnout počet hopů: když přijde `TTL=118`, pravděpodobně vyšlo ze 128 a prošlo 10 routery.

### Využití v traceroute

[[traceroute]] TTL **záměrně zneužívá** – posílá pakety s TTL 1, 2, 3… a z hlášení Time Exceeded skládá seznam routerů po cestě.

### Název u IPv6

V [[IPv6]] se stejné pole jmenuje **Hop Limit** – je to přesnější, protože se nikdy nejednalo o čas, ale o počet skoků.

### Jiné významy TTL

Pozor, zkratka se používá i jinde – např. u [[DNS]] záznamů TTL říká, **jak dlouho se smí odpověď držet v cache** (v sekundách).

**Souvisí:** [[ping]], [[traceroute]], [[ICMP]], [[router]], [[IPv6]], [[DNS]]
