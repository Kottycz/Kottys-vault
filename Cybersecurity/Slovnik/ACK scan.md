---
aliases: [-sA, TCP ACK]
tags: [slovnik]
---

# ACK scan (`-sA`)

Pošle paket s příznakem [[ACK]]; cíl odpoví [[RST]] **bez ohledu na stav portu**.

*Příklad: `sudo nmap -sA MACHINE_IP`.*

---

## Podrobně

- neříká, zda je port otevřený
- porty jsou `unfiltered` (neblokované), jinak `filtered`
- slouží ke **zmapování pravidel firewallu**
- podobný [[TCP ACK ping]]

**Souvisí:** [[skenování portů]], [[Window scan]], [[ACK]], [[RST]], [[firewall]], [[stavy portů]], [[TCP ACK ping]]
