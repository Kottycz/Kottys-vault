---
aliases: [TCP SYN ping, -PS, SYN ping]
tags: [slovnik]
---

# TCP SYN ping (`-PS`)

Metoda [[nmap|Nmapu]], která pošle paket s příznakem [[SYN]] na TCP port a čeká na **jakoukoli odpověď** – tím pozná, že je hostitel živý.

*Příklad: `sudo nmap -PS -sn 10.10.68.220/24` pošle SYN na port 80 všech adres v podsíti.*

---

## Podrobně

| Odpověď cíle | Význam |
| :-- | :-- |
| **SYN/ACK** | port otevřený, hostitel živý |
| **[[RST]]** | port zavřený, hostitel **přesto živý** |
| žádná | offline / blokováno |

- výchozí port **80**; zadání: `-PS21`, `-PS21-25`, `-PS80,443,8080`
- stav portu **není podstatný**, jen že odpověď přišla
- privilegovaný uživatel nemusí dokončit [[3-way handshake]]; neprivilegovaný ho dokončí vždy, pokud je port otevřený

**Souvisí:** [[TCP ACK ping]], [[UDP ping]], [[ping scan]], [[zjišťování živých hostitelů]], [[3-way handshake]], [[TCP]]
