---
aliases: [Virtual Private Network]
tags: [slovnik]
---

# VPN

**Virtual Private Network** – šifrovaný tunel přes veřejnou síť. Zařízení se chová, jako by bylo připojené přímo do vzdálené sítě.

---

## Podrobně

### Princip

Data se zabalí do dalšího, zašifrovaného paketu (tunelování). Poskytovatel vidí jen, že komunikuješ s VPN serverem – ne co posíláš ani kam.

```
Bez VPN:  PC ──────────── internet ──────► cíl
                    (poskytovatel vidí vše)

S VPN:    PC ══šifrovaný tunel══► VPN server ──► cíl
                    (poskytovatel vidí jen tunel)
```

### Dva hlavní typy

| Typ | Použití |
| :-- | :-- |
| **Remote access** | jednotlivec se připojí do firemní sítě z domova |
| **Site-to-site** | trvale propojí dvě pobočky přes internet ([[WAN]]) |

Site-to-site VPN je levnější náhrada pronajatých okruhů.

### Protokoly

| Protokol | Popis |
| :-- | :-- |
| **IPsec** | standard pro site-to-site, šifruje na síťové vrstvě |
| **OpenVPN** | otevřený, běží nad [[TLS]] |
| **WireGuard** | moderní, jednoduchý a rychlý |
| **L2TP, PPTP** | starší, PPTP je nebezpečný |

### K čemu se používá

- Přístup do firemní sítě z domova (práce na dálku)
- Propojení poboček
- Ochrana na veřejné Wi-Fi
- Obcházení geografických omezení

### Co VPN neřeší

- **Nedělá tě anonymním** – provozovatel VPN vidí to, co předtím viděl poskytovatel
- Nechrání před malwarem ani phishingem
- Přidává [[latency|latenci]] a snižuje [[throughput]]
- Kvůli režii tunelu má menší [[MTU]] (proto někdy problémy s načítáním stránek – řeší se MSS clampingem)

### Site-to-site vs. remote access

| | Site-to-site | Remote access |
| :-- | :-- | :-- |
| spojuje | dvě sítě (pobočka – centrála) | jednoho uživatele se sítí firmy |
| kdo tunel vytváří | routery nebo firewally | klient na PC (AnyConnect, WireGuard, OpenVPN) |
| uživatel to pozná | ne, je to transparentní | ano, musí se připojit |

### IPsec

Nejčastější protokol pro site-to-site VPN. Zajišťuje:

- **důvěrnost** – šifrování (AES),
- **integritu** – kontrola, že data nikdo nezměnil (hash),
- **ověření** – obě strany prokážou, kým jsou (sdílený klíč nebo certifikát).

### Split tunneling

Při remote access VPN jde buď **všechen** provoz přes firmu (full tunnel), nebo jen provoz do firemní sítě a zbytek přímo do internetu (split tunnel). Split tunnel šetří linku firmy, full tunnel je bezpečnější.

**Souvisí:** [[WAN]], [[TLS]], [[MTU]], [[MSS]], [[NAT]]
