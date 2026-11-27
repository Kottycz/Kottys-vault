---
aliases: [Internet Control Message Protocol, ICMPv4, ICMPv6]
tags: [slovnik]
---

# ICMP

**Internet Control Message Protocol** – služební protokol síťové vrstvy. Posílá zprávy o chybách a stavu sítě (např. "cíl je nedostupný"). Nepřenáší uživatelská data.

---

## Podrobně

### K čemu slouží

IP samo neumí hlásit problémy. Když paket nelze doručit, ICMP o tom pošle zprávu zpátky odesílateli. Na ICMP stojí i diagnostické nástroje [[ping]] a [[traceroute]].

### Hlavní typy zpráv

| Zpráva | Význam |
| :-- | :-- |
| **Echo Request / Echo Reply** | "jsi tam?" / "jsem" – základ [[ping\|pingu]] |
| **Destination Unreachable** | cíl nedostupný (síť, host, port, protokol) |
| **Time Exceeded** | vypršel [[TTL]] – využívá [[traceroute]] |
| **Redirect** | "posílej to raději přes jiný router" |

### Verze

- **ICMPv4** – pro [[IPv4]]
- **ICMPv6** – pro [[IPv6]]. Má stejné funkce, ale navíc na něm stojí [[NDP]] (zprávy [[RS]], [[RA]], [[NS]], [[NA]]) – tedy to, co v IPv4 dělá [[ARP]] a [[DHCP]].

U IPv6 tedy ICMP **není volitelné** – bez něj síť vůbec nefunguje (proto se nesmí kompletně blokovat na firewallu).

### Ping

`ping 8.8.8.8` pošle Echo Request a čeká na Echo Reply. Měří:

- jestli je cíl dostupný
- **RTT** (round-trip time) – jak dlouho trvala cesta tam a zpět
- ztrátovost paketů

### Traceroute

Využívá [[TTL]]: pošle paket s TTL=1 (první router ho zahodí a pošle Time Exceeded), pak TTL=2, TTL=3… Postupně se tak vypíšou všechny routery po cestě k cíli.

### Proč se někdy blokuje

ICMP může útočníkovi prozradit strukturu sítě (kdo existuje, kudy vede cesta), proto ho některé [[firewall|firewally]] blokují. Pak `ping` nefunguje, i když zařízení běží.

### ICMP zprávy destination unreachable

| Kód | Význam |
| :-- | :-- |
| 0 | síť nedosažitelná |
| 1 | host nedosažitelný |
| 3 | port nedosažitelný |

Zprávu posílá [[router]] (nebo cílový host), který paket nemohl doručit. Na Cisco se v `ping` projeví jako **U**.

### ICMPv6 je důležitější

V [[IPv6]] ICMP nedělá jen diagnostiku. Zprávy [[NDP]] ([[RS]], [[RA]], [[NS]], [[NA]]) jsou ICMPv6 a nahrazují [[ARP]] i část [[DHCP]]. Kdo v IPv6 síti zablokuje celé ICMPv6, síť přestane fungovat.

### Time exceeded

Typ 11. Router ho pošle, když paketu klesne [[TTL]] na 0. Právě na tom stojí [[traceroute]].

**Souvisí:** [[ping]], [[traceroute]], [[TTL]], [[NDP]], [[IPv4]], [[IPv6]], [[firewall]]
