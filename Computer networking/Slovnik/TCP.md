---
aliases: [Transmission Control Protocol]
tags: [slovnik]
---

# TCP

**Transmission Control Protocol** – spolehlivý, spojovaný protokol transportní vrstvy (OSI 4). Před přenosem naváže spojení, potvrzuje doručení a zachovává pořadí dat.

---

## Podrobně

### Co řeší

IP ([[IPv4]]/[[IPv6]]) samo o sobě nezaručuje nic – pakety se můžou ztratit, přijít v jiném pořadí nebo dorazit dvakrát. TCP tohle všechno řeší nad IP, aby aplikace dostala data přesně tak, jak byla odeslána.

### Vlastnosti

- **Spojovaný (connection-oriented)** – před přenosem se naváže spojení pomocí [[3-way handshake]] (SYN → SYN-ACK → ACK), na konci se ukončí (FIN).
- **Spolehlivý** – příjemce potvrzuje přijatá data (ACK). Když potvrzení nedorazí, odesílatel segment pošle znovu.
- **Zachovává pořadí** – každý segment má pořadové číslo (sequence number), příjemce je složí ve správném pořadí.
- **Řízení toku** – [[sliding window]]: příjemce oznamuje, kolik dat ještě zvládne přijmout.
- **Řízení zahlcení** – [[slow start]] a další algoritmy postupně zvyšují rychlost odesílání podle stavu sítě.

### Hlavička

Má **20 bajtů** (minimálně), obsahuje mimo jiné:

| Pole | Význam |
| :-- | :-- |
| Zdrojový a cílový [[port]] | identifikuje aplikaci na obou stranách |
| Sequence number | pořadové číslo prvního bajtu v segmentu |
| Acknowledgment number | číslo dalšího očekávaného bajtu |
| Flags | SYN, ACK, FIN, RST, PSH, URG |
| Window | kolik dat může příjemce přijmout |
| Checksum | kontrola integrity |

### PDU

Jednotka dat TCP se nazývá **segment** (viz [[PDU]]).

### Kde se používá

Všude, kde nesmí chybět ani bajt: [[HTTP]]/[[HTTPS]] (web), [[FTP]] (přenos souborů), [[SMTP]]/[[POP3]]/[[IMAP]] (e-mail), SSH.

### TCP vs. UDP

| | TCP | [[UDP]] |
| :-- | :-- | :-- |
| Spojení | ano (handshake) | ne |
| Spolehlivost | potvrzuje, opakuje | nepotvrzuje |
| Pořadí | zachovává | nezaručuje |
| Hlavička | 20 B | 8 B |
| Rychlost | pomalejší | rychlejší |
| Typické užití | web, e-mail, soubory | streaming, hry, [[DNS]], VoIP |

**Souvisí:** [[UDP]], [[3-way handshake]], [[sliding window]], [[slow start]], [[port]], [[socket]], [[MSS]], [[ISN]]
