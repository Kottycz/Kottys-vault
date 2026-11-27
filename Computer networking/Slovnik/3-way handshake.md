---
aliases: [třícestný handshake, trojcestný handshake, handshake]
tags: [slovnik]
---

# 3-way handshake

**Třícestný handshake** – tři zprávy, kterými [[TCP]] naváže spojení, než začne posílat data. Obě strany si přitom vymění počáteční pořadová čísla ([[ISN]]).

---

## Podrobně

### Průběh

```
Klient                                Server

  |  1. SYN  (seq = x)                  |
  | ---------------------------------> |   "chci se spojit"
  |                                     |
  |  2. SYN-ACK (seq = y, ack = x+1)   |
  | <--------------------------------- |   "ok, já taky"
  |                                     |
  |  3. ACK  (ack = y+1)               |
  | ---------------------------------> |   "potvrzeno"
  |                                     |
  |  ===== spojení navázáno =====      |
```

1. **SYN** – klient pošle svoje počáteční pořadové číslo (x)
2. **SYN-ACK** – server potvrdí (x+1) a pošle svoje vlastní číslo (y)
3. **ACK** – klient potvrdí serverovo číslo (y+1)

Teprve pak se posílají data.

### K čemu to je

- Obě strany ověří, že ta druhá **existuje a je ochotná komunikovat**
- Dohodnou se na **počátečních pořadových číslech** ([[ISN]]) pro číslování dat
- Vymění si parametry jako [[MSS]] a velikost okna

### Ukončení spojení (4-way)

Ukončení je čtyřcestné, protože každá strana ukončuje svůj směr zvlášť:

```
FIN → ACK → FIN → ACK
```

### Bezpečnost – SYN flood

Útočník pošle spoustu SYN a nikdy neodpoví na SYN-ACK. Server drží polootevřená spojení a vyčerpá si prostředky (typ DoS útoku). Obrana: SYN cookies, limity.

### Jak to vypadá ve Wiresharku

Filtr `tcp.flags.syn == 1` ukáže první dvě zprávy. Wireshark ukazuje **relativní** sekvenční čísla, takže SYN má Seq=0, SYN-ACK má Seq=0 a Ack=1, poslední ACK má Seq=1 a Ack=1. Skutečná čísla jsou náhodná ([[ISN]]).

```
Klient → Server   [SYN]      Seq=0
Server → Klient   [SYN, ACK] Seq=0 Ack=1
Klient → Server   [ACK]      Seq=1 Ack=1
```

### Stavy TCP spojení

| Stav | Kdo | Význam |
| :-- | :-- | :-- |
| LISTEN | server | čeká na SYN na otevřeném [[port|portu]] |
| SYN-SENT | klient | poslal SYN, čeká na SYN-ACK |
| SYN-RECEIVED | server | poslal SYN-ACK, čeká na ACK |
| ESTABLISHED | oba | spojení navázané, posílají se data |
| TIME-WAIT | ten, kdo zavíral | chvíli čeká, aby zachytil zpožděné pakety |

Stavy uvidíš na PC příkazem `netstat -an`.

### Když handshake nevyjde

- **port je zavřený** → server odpoví příznakem **RST** (reset), spojení se hned odmítne,
- **nepřijde nic** → paket zahodil [[firewall]] nebo cíl neexistuje, klient SYN po čase zopakuje a pak to vzdá (timeout),
- [[UDP]] žádný handshake nemá, proto je rychlejší, ale nespolehlivý.

**Souvisí:** [[TCP]], [[ISN]], [[MSS]], [[sliding window]]
