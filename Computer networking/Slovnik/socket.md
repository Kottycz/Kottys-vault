---
aliases: [sokety, socket pair]
tags: [slovnik]
---

# socket

**Kombinace [[IP adresa|IP adresy]] a [[port|portu]]** – jednoznačně identifikuje jeden konec síťového spojení. Zapisuje se `192.168.1.10:443`.

---

## Podrobně

### Co identifikuje

```
192.168.1.10 : 443
└── IP ────┘  └port┘
  který           která
  počítač         aplikace
```

IP adresa sama určí jen stroj, port jen službu – teprve dohromady jednoznačně řeknou, s čím se komunikuje.

### Socket pair

Celé spojení určuje **dvojice socketů**:

```
Klient 192.168.1.10:51234  ←→  Server 93.184.216.34:443
```

Tahle čtveřice (zdrojová IP, zdrojový port, cílová IP, cílový port) je jedinečná – díky tomu může mít prohlížeč otevřených deset spojení na stejný server naráz, každé s jiným zdrojovým portem.

### Zobrazení otevřených socketů

- Windows: `netstat -an`
- Linux: `ss -tuln` nebo `netstat -tuln`

Vidíš tam, co na počítači naslouchá a kam je připojený – užitečné při hledání, která aplikace zabírá port.

### Socket jako programátorský pojem

V programování je socket **rozhraní operačního systému** pro síťovou komunikaci. Aplikace vytvoří socket, naváže ho na port (`bind`), naslouchá (`listen`) a přijímá spojení (`accept`) – nebo se sama připojí (`connect`). Pak se na něj jen zapisuje a čte jako do souboru.

### Stavy socketu (TCP)

`LISTEN` (čeká na spojení), `ESTABLISHED` (spojeno), `TIME_WAIT` (po ukončení chvíli drží), a další – vidíš je právě ve výstupu `netstat`.

### Jak server rozliší klienty

Webový server poslouchá na jednom socketu `203.0.113.10:443`, ale obsluhuje tisíce klientů. Každé spojení je odlišené **dvojicí socketů**:

```
192.168.1.5:50123  ↔  203.0.113.10:443
192.168.1.5:50124  ↔  203.0.113.10:443   ← jiná záložka prohlížeče
10.0.0.7:61000     ↔  203.0.113.10:443   ← jiný klient
```

Klient dostane od systému náhodný **dynamický port** (49152–65535), takže dvě spojení ze stejného PC se nepletou.

### Socket a NAT

[[NAT]] (PAT) přepisuje zdrojový socket: soukromou IP i port nahradí veřejnou IP a jiným portem a pamatuje si, který vnitřní socket patří ke kterému vnějšímu.

**Souvisí:** [[port]], [[IP adresa]], [[TCP]], [[UDP]]
