---
aliases: [Internet Assigned Numbers Authority]
tags: [slovnik]
---

# IANA

**Internet Assigned Numbers Authority** – organizace přidělující celosvětově jedinečná čísla a jména v internetu: [[port|porty]], [[IP adresa|IP adresy]] a domény nejvyšší úrovně.

---

## Podrobně

### Co spravuje

| Oblast | Příklad |
| :-- | :-- |
| **Čísla portů** | 80 = [[HTTP]], 443 = [[HTTPS]] |
| **IP adresní bloky** | přiděluje je regionálním registrům |
| **Domény nejvyšší úrovně** | .com, .cz, .org |
| **Čísla protokolů** | 6 = [[TCP]], 17 = [[UDP]], 1 = [[ICMP]] |

### Regionální registry (RIR)

IANA nepřiděluje adresy koncovým zákazníkům – rozdá velké bloky pěti regionálním registrům, ty je dělí poskytovatelům:

| Registr | Region |
| :-- | :-- |
| **RIPE NCC** | Evropa (tedy i ČR) |
| ARIN | Severní Amerika |
| APNIC | Asie a Pacifik |
| LACNIC | Latinská Amerika |
| AFRINIC | Afrika |

### Registrované porty

Právě IANA rozhoduje, které aplikaci patří který port v rozsahu 1024–49151 (registered ports) – proto je seznam portů jednotný na celém světě.

### Vztah k ICANN

IANA dnes funguje pod organizací **ICANN**, která spravuje jmenný systém internetu ([[DNS]]).

### Co IANA přidělila, co se učíš

| Číslo | Příklad |
| :-- | :-- |
| [[port|porty]] | 22 SSH, 53 DNS, 80 HTTP, 443 HTTPS |
| privátní rozsahy IPv4 | 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16 |
| čísla protokolů v IP hlavičce | 1 ICMP, 6 TCP, 17 UDP |
| [[EtherType]] hodnoty spravuje [[IEEE]], ne IANA | — |

### Rozsahy portů

| Rozsah | Název | Příklad |
| :-- | :-- | :-- |
| 0–1023 | well-known (systémové) | 80 HTTP |
| 1024–49151 | registrované | 3389 RDP |
| 49152–65535 | dynamické / privátní | náhodný port klienta |

### Vyčerpání IPv4

V roce 2011 IANA rozdala regionálním registrům poslední volné bloky IPv4 adres. Od té doby se nové IPv4 adresy získávají těžko, proto [[NAT]] a přechod na [[IPv6]].

**Souvisí:** [[port]], [[IP adresa]], [[DNS]], [[IETF]]
