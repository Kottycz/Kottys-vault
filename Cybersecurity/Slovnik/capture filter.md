---
aliases: [zachytávací filtr, capture filtr, BPF]
tags: [slovnik]
---

# capture filter

Filtr, který se nastaví **před zachytáváním** a uloží jen provoz, který mu odpovídá – zbytek se **zahodí**.

*Příklad: `tcp port 80` – zachytí jen TCP provoz na portu 80.*

---

## Podrobně

- syntaxe **BPF** (Berkeley Packet Filter), jiná než [[display filter]]
- **Scope:** `host`, `net`, `port`, `portrange`
- **Direction:** `src`, `dst`, `src or dst`, `src and dst`
- **Protocol:** `ether`, `wlan`, `ip`, `ip6`, `arp`, `rarp`, `tcp`, `udp`
- během zachytávání **nejde měnit**
- co se nezachytí, **nejde vrátit** → používají ho hlavně zkušení
- šetří výkon a paměť
- nápověda: **Capture → Capture Filters**, nastavení v `Ctrl+K`

**Souvisí:** [[display filter]], [[Wireshark]], [[PCAP]]
