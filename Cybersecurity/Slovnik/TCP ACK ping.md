---
aliases: [TCP ACK ping, -PA, ACK ping]
tags: [slovnik]
---

# TCP ACK ping (`-PA`)

Metoda [[nmap|Nmapu]], která pošle paket s příznakem [[ACK]] (bez existujícího spojení); živý cíl odpoví [[RST]].

*Příklad: `sudo nmap -PA -sn 10.10.68.220/24` → 5 živých hostitelů.*

---

## Podrobně

- vyžaduje **privilegovaného uživatele** (jinak se Nmap pokusí o 3-way handshake)
- cíl odpoví **RST**, protože ACK **nepatří k žádnému probíhajícímu spojení**
- tato odpověď stačí k potvrzení, že je cíl aktivní
- výchozí port **80**; zadání `-PA21`, `-PA21-25`, `-PA80,443,8080`
- Nmap posílá každý paket **dvakrát**
- hostitelé, kteří neodpoví, jsou offline nebo nepřístupní
- hodí se, když firewall blokuje SYN nebo ICMP

**Souvisí:** [[TCP SYN ping]], [[UDP ping]], [[ping scan]], [[zjišťování živých hostitelů]], [[3-way handshake]], [[TCP]]
