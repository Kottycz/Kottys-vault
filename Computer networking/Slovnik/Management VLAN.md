---
aliases: [správcovská VLAN, VLAN pro správu]
tags: [slovnik]
---

# Management VLAN

**Management VLAN** – [[VLAN]], přes kterou se dostaneš ke správě switche (Telnet, SSH, web). Switch v ní má [[SVI]] s IP adresou. Příklad: VLAN 99 jen pro adminy.

---

## Podrobně

- správa switche jde přes SVI s IP adresou v této VLAN (viz [[Sprava_switche_SVI]]),
- ve výchozím stavu je to [[Default VLAN|VLAN 1]],
- z bezpečnostních důvodů je dobré použít jinou než VLAN 1.

**Souvisí:** [[VLAN]], [[SVI]], [[Default VLAN]], [[SSH]], [[Telnet]]
