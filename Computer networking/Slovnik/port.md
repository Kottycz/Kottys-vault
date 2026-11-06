---
aliases: [porty, číslo portu]
tags: [slovnik]
---

# port

**Číslo (0–65535) identifikující konkrétní aplikaci nebo službu** na zařízení. Pracuje na transportní vrstvě ([[TCP]]/[[UDP]]) – [[IP adresa]] určí počítač, port určí program v něm.

---

## Podrobně

### Analogie

IP adresa = adresa domu, port = číslo bytu. Bez portu by data dorazila na správný počítač, ale nevědělo by se, které aplikaci je předat.

### Rozdělení rozsahů

| Rozsah | Název | Použití |
| :-- | :-- | :-- |
| 0–1023 | **Well-known** | standardní služby (web, e-mail…), vyžadují admin práva |
| 1024–49151 | **Registered** | registrované aplikace (databáze, hry) |
| 49152–65535 | **Dynamic / private** | dočasné porty klientů |

### Nejdůležitější porty (na test)

| Port | Protokol | Služba |
| :-- | :-- | :-- |
| 20, 21 | TCP | [[FTP]] (data, řízení) |
| 22 | TCP | SSH |
| 23 | TCP | Telnet (nešifrovaný) |
| 25 | TCP | [[SMTP]] |
| 53 | UDP/TCP | [[DNS]] |
| 67, 68 | UDP | [[DHCP]] (server, klient) |
| 80 | TCP | [[HTTP]] |
| 110 | TCP | [[POP3]] |
| 143 | TCP | [[IMAP]] |
| 443 | TCP | [[HTTPS]] |

### Zdrojový vs. cílový port

Když prohlížeč načítá web:

```
Klient 192.168.1.10 : 51234   →   Server 93.184.216.34 : 443
        └ dynamický ┘                        └ well-known ┘
```

Klient si vezme náhodný dynamický port, server naslouchá na známém. Odpověď se pak vrací obráceně. Dvojice IP + port se nazývá [[socket]].

### Port forwarding

Když je v cestě [[NAT]], zvenku nelze oslovit vnitřní zařízení. Port forwarding nastaví pravidlo "co přijde na veřejný port X, pošli na vnitřní IP:port Y" – používá se např. pro herní servery.

**Souvisí:** [[socket]], [[TCP]], [[UDP]], [[IP adresa]], [[NAT]]
