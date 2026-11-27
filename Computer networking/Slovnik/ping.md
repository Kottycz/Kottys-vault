---
tags: [slovnik]
---

# ping

**Diagnostický nástroj**, který ověří dostupnost zařízení. Pošle [[ICMP]] Echo Request a čeká na Echo Reply. Měří dobu odezvy a ztrátovost.

---

## Podrobně

### Co vypisuje

```
ping 8.8.8.8

Odpověď od 8.8.8.8: bajty=32 čas=12ms TTL=118
Odpověď od 8.8.8.8: bajty=32 čas=11ms TTL=118

Statistika: Odesláno = 4, Přijato = 4, Ztraceno = 0 (0% ztráta)
Přibližná doba do cíle: min = 11ms, max = 13ms, průměr = 12ms
```

| Údaj | Význam |
| :-- | :-- |
| **čas** | RTT – doba cesty tam a zpět (viz [[latency]]) |
| **[[TTL]]** | zbývající počet hopů – z něj se dá odhadnout, přes kolik routerů to šlo |
| **ztráta** | kolik paketů se nevrátilo (indikuje problém na lince) |

### Typické chyby

| Hláška | Znamená |
| :-- | :-- |
| **Request timed out** | odpověď nedorazila – cíl je vypnutý, blokuje ICMP, nebo je cesta přerušená |
| **Destination host unreachable** | [[router]] neví, kudy paket poslat |
| **Neznámý hostitel** | selhal překlad jména přes [[DNS]] |

### Postup při hledání problému

1. `ping 127.0.0.1` – funguje můj vlastní TCP/IP stack? (viz [[loopback]])
2. `ping` na vlastní IP – je v pořádku moje [[NIC|síťovka]]?
3. `ping` na [[default gateway|výchozí bránu]] – vidím svůj router?
4. `ping 8.8.8.8` – mám internet?
5. `ping seznam.cz` – funguje mi [[DNS]]?

Kde to selže, tam je problém.

### Užitečné přepínače

- `ping -t <cíl>` – pinguje donekonečna (Windows), ukončí se Ctrl+C
- `ping -n 10 <cíl>` – počet paketů (Windows), na Linuxu `-c 10`
- `ping -l 1500 <cíl>` – velikost paketu (test [[MTU]])

### Pozor

Když ping neprojde, **neznamená to nutně, že zařízení nefunguje** – spousta firewallů ICMP blokuje z bezpečnostních důvodů.

### Ping z Cisco routeru – výstup

```
R1# ping 192.168.2.10
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.2.10, timeout is 2 seconds:
.!!!!
Success rate is 80 percent (4/5), round-trip min/avg/max = 1/1/2 ms
```

| Znak | Význam |
| :-- | :-- |
| `!` | odpověď přišla |
| `.` | vypršel čas |
| `U` | cíl nedosažitelný (ICMP unreachable) |

První `.` je obvykle kvůli [[ARP]], router teprve zjišťuje MAC adresu.

### Ping a TTL

Z TTL v odpovědi se dá odhadnout systém cíle: Windows začíná na **128**, Linux a většina zařízení na **64**, Cisco na **255**. Odečteš skoky po cestě.

### Když ping nefunguje, ale služba ano

Mnoho [[firewall|firewallů]] (i Windows Defender) ICMP blokuje. Neúspěšný ping proto neznamená vždy, že cíl neexistuje. Ověř to jinak, např. přes `Test-NetConnection server -Port 443`.

**Souvisí:** [[ICMP]], [[traceroute]], [[TTL]], [[latency]], [[default gateway]], [[loopback]], [[echo request]], [[rozšířený ping]]
