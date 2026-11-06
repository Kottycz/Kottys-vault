---
aliases: [-sW, TCP Window]
tags: [slovnik]
---

# Window scan (`-sW`)

Jako [[ACK scan]], ale zkoumá pole **TCP Window** v odpovědi [[RST]].

*Příklad: `sudo nmap -sW MACHINE_IP`.*

---

## Podrobně

- u některých systémů odhalí otevřený port
- bez firewallu nepřináší nic navíc
- za firewallem odliší porty, které firewall neblokuje

**Souvisí:** [[skenování portů]], [[ACK scan]], [[RST]], [[firewall]], [[hlavička TCP]]
