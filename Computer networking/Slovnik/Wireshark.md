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

**Souvisí:** [[sniffer]], [[Telnet]], [[SSH]], [[TCP]], [[MITM]]
