---
aliases: [Neighbor Discovery Protocol, objevování sousedů]
tags: [slovnik]
---

# NDP

**Neighbor Discovery Protocol** – protokol [[IPv6]], který zajišťuje objevování sousedů a routerů. Nahrazuje to, co v [[IPv4]] dělal [[ARP]] a částečně [[DHCP]]. Běží nad ICMPv6.

---

## Podrobně

### Čtyři hlavní zprávy

| Zkratka | Název | K čemu |
| :-- | :-- | :-- |
| **[[RS]]** | Router Solicitation | zařízení se ptá: "je tu router?" |
| **[[RA]]** | Router Advertisement | router oznamuje prefix a sám sebe jako bránu |
| **[[NS]]** | Neighbor Solicitation | "kdo má tuhle adresu?" (náhrada ARP Requestu) |
| **NA** | Neighbor Advertisement | "to jsem já, tady je moje MAC" (náhrada ARP Reply) |

### Co všechno NDP dělá

1. **Zjištění MAC adresy souseda** – přes NS/NA (místo [[ARP]])
2. **Objevení routeru a prefixu** – přes RS/RA, základ [[SLAAC]]
3. **[[DAD]]** – ověření, že adresu nemá nikdo jiný
4. **Detekce nedostupnosti souseda** – zjistí, že soused přestal odpovídat
5. **Přesměrování** – router může oznámit lepší cestu

### Rozdíl oproti ARP

| | [[ARP]] (IPv4) | NDP (IPv6) |
| :-- | :-- | :-- |
| Vrstva | přímo nad Ethernetem (vl. 2) | nad ICMPv6 (vl. 3) |
| Dotaz jde | [[broadcast|broadcastem]] všem | [[multicast|multicastem]] jen relevantním |
| Funkce | jen překlad IP→MAC | + objevení routeru, DAD, SLAAC |

Multicast je efektivnější – dotaz nevyruší celou síť, ale jen zařízení se shodným koncem adresy (solicited-node multicast).

### Bezpečnost

Stejně jako ARP nemá NDP ověřování – lze ho zneužít (podvržená RA, NA spoofing). Obrana: **RA Guard**, **SEND** (Secure Neighbor Discovery), ND inspection na [[switch|switchích]].

### Neighbor cache

Obdoba [[ARP]] tabulky v IPv6. Ukládá dvojice IPv6 adresa ↔ MAC adresa sousedů.

| Kde | Příkaz |
| :-- | :-- |
| Windows | `netsh interface ipv6 show neighbors` |
| Linux | `ip -6 neigh` |
| Cisco | `show ipv6 neighbors` |

### Pátá zpráva: Redirect

Kromě RS, RA, NS a NA má NDP ještě **Redirect** (ICMPv6 typ 137). Router jí řekne hostiteli: „k tomuhle cíli máš lepší cestu přes jiný router ve stejné síti".

### Čísla zpráv (ICMPv6 typ)

| Zpráva | Typ |
| :-- | :-- |
| [[RS]] | 133 |
| [[RA]] | 134 |
| [[NS]] | 135 |
| [[NA]] | 136 |
| Redirect | 137 |

**Souvisí:** [[IPv6]], [[ARP]], [[RS]], [[RA]], [[NS]], [[DAD]], [[SLAAC]], [[ICMP]]
