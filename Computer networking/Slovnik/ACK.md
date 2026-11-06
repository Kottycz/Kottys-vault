---
aliases: [Acknowledgment, potvrzení, SYN, FIN, RST, TCP příznaky]
tags: [slovnik]
---

# ACK

**Acknowledgment** – potvrzení příjmu dat v [[TCP]]. Příznak v hlavičce, kterým příjemce oznamuje "tohle mi dorazilo".

---

## Podrobně

### Jak potvrzování funguje

Příjemce v poli **Acknowledgment number** posílá **číslo dalšího očekávaného bajtu**:

```
Přijal jsem bajty 1–1000  →  ACK = 1001
                              "další čekám od 1001"
```

Když odesílatel potvrzení nedostane do vypršení časovače, segment pošle znovu.

### Příznaky (flags) v TCP hlavičce

| Příznak | Význam |
| :-- | :-- |
| **SYN** | synchronizace – navázání spojení ([[3-way handshake]]) |
| **ACK** | potvrzení přijatých dat |
| **FIN** | ukončení spojení |
| **RST** | okamžité zrušení spojení (chyba, odmítnutí) |
| **PSH** | předej data aplikaci hned, nečekej na buffer |
| **URG** | urgentní data |

### Kde se s nimi setkáš

```
Navázání:   SYN  →  SYN-ACK  →  ACK
Přenos:     data →  ACK      →  data → ACK ...
Ukončení:   FIN  →  ACK      →  FIN  → ACK
```

Když se pokusíš připojit na zavřený [[port]], server odpoví **RST** – proto "connection refused" přijde okamžitě.

### Kumulativní potvrzování

ACK potvrzuje **všechno až do dané pozice** – jedno potvrzení tedy pokryje víc segmentů najednou. Když chybí kus uprostřed, řeší to [[SACK]].

### Duplicitní ACK

Když příjemce dostane segment mimo pořadí, pošle znovu poslední ACK. **Tři duplicitní ACK** za sebou odesílatel chápe jako signál ztráty a segment pošle znovu, aniž by čekal na vypršení časovače (fast retransmit).

**Souvisí:** [[TCP]], [[3-way handshake]], [[SACK]], [[sliding window]], [[ISN]]
