---
aliases: [Initial Sequence Number, počáteční pořadové číslo]
tags: [slovnik]
---

# ISN

**Initial Sequence Number** – náhodně zvolené počáteční pořadové číslo, které si obě strany [[TCP]] vymění při [[3-way handshake]]. Od něj se pak číslují všechny přenášené bajty.

---

## Podrobně

### Kde se objeví

```
Klient  →  SYN  (seq = x)      ← x je ISN klienta
Server  →  SYN-ACK (seq = y, ack = x+1)   ← y je ISN serveru
Klient  →  ACK  (ack = y+1)
```

Každá strana má **vlastní ISN** – číslování obou směrů je nezávislé.

### Jak se dál počítá

Od ISN se přičítá počet přenesených bajtů:

```
ISN = 1000
1. segment: seq = 1001, 500 B dat
2. segment: seq = 1501, 300 B dat
3. segment: seq = 1801, ...
```

Příjemce podle toho pozná pořadí a chybějící kusy.

### Proč je náhodné

Kdyby ISN začínalo vždy od nuly nebo šlo předpovědět, útočník by mohl **podvrhnout segmenty do cizího spojení** (TCP session hijacking) – stačilo by mu uhodnout očekávané pořadové číslo. Proto se ISN generuje náhodně.

Historicky to byl reálný problém (Mitnickův útok v roce 1994), dnešní systémy používají kryptograficky silné generátory.

### Souvislost s handshakem

Hlavním smyslem [[3-way handshake]] je právě **synchronizace ISN** obou stran – proto se ten příznak jmenuje **SYN** (synchronize).

**Souvisí:** [[TCP]], [[3-way handshake]], [[sliding window]]
