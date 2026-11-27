---
aliases: []
tags: [slovnik]
---

# Wireshark

**Wireshark** – program pro **zachytávání a rozbor síťového provozu** (packet [[sniffer]]). Příklad: zachytíš [[Telnet]] relaci a v čistém textu v ní uvidíš jméno `admin` a heslo `ccna`.

---

## Podrobně

### K čemu slouží

- diagnostika sítě (co se opravdu posílá, kde se ztrácí pakety),
- učení protokolů (každá vrstva rozbalená v panelu),
- bezpečnostní analýza – ukáže, **co jde po síti nešifrovaně**.

### Ukázka z kurzu

| | [[Telnet]] | [[SSH]] |
| :-- | :-- | :-- |
| Provoz | `TELNET Data`, port 23 | `SSHv2 Encrypted packet`, port 22 |
| **Follow TCP Stream** | čitelné přihlášení i data | nečitelný šifrovaný obsah |
| Co vidí útočník | jméno, heslo, příkazy | jen IP adresy a objem |

### Užitečné funkce

- **Display filter** (např. `tcp.stream eq 0`, `ip.addr == 192.168.10.10`),
- **Follow TCP Stream** – složí celý rozhovor do čitelného textu,
- uložení do `.pcapng`.

### Nejpoužívanější filtry

| Filtr | Co ukáže |
| :-- | :-- |
| `ip.addr == 192.168.1.10` | provoz z/na adresu |
| `tcp.port == 80` | provoz na port 80 |
| `icmp` | ping a ICMP zprávy |
| `arp` | ARP |
| `dns` | DNS dotazy a odpovědi |
| `dhcp` | DHCP (DORA) |
| `tcp.flags.syn == 1` | navazování TCP spojení |
| `!(arp or dns)` | vše kromě ARP a DNS |

### Tři části okna

1. **seznam paketů** – čas, zdroj, cíl, protokol, info,
2. **detail paketu** – rozbalené vrstvy (Ethernet → IP → TCP → aplikace),
3. **bajty** – surová data v hex.

V detailu paketu přesně uvidíš [[zapouzdření]] – každá vrstva je zvlášť.

### Na co si dát pozor

Zachytávat provoz v cizí síti bez svolení je nelegální. Ve škole a doma jen na vlastních zařízeních nebo se souhlasem správce.

**Souvisí:** [[sniffer]], [[Telnet]], [[SSH]], [[TCP]], [[MITM]]
