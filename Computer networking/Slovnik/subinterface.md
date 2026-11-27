---
aliases: [sub-interface, podrozhraní, sub-interfaces, subinterfaces]
tags: [slovnik]
---

# subinterface

**Subinterface** (podrozhraní) – softwarové virtuální rozhraní vytvořené na jednom fyzickém rozhraní routeru. Příklad: `G0/0/1.10` je podrozhraní fyzického `G0/0/1` pro VLAN 10.

---

## Podrobně

- v [[Router-on-a-Stick]] má každá [[VLAN]] vlastní podrozhraní,
- každé podrozhraní se konfiguruje **nezávisle**: má vlastní [[IP adresa|IP adresu]] a přiřazení k VLAN,
- příkazy: `interface interface-id.subinterface-id`, `encapsulation dot1q vlan_id [native]`, `ip address ip-address subnet-mask`,
- přijme rámec s tagem své VLAN a odešle rámec s tagem cílové VLAN,
- fyzické rozhraní se zapíná zvlášť (`no shutdown`).

### Pojmenování

`G0/0/1.10` = fyzické rozhraní `G0/0/1`, podrozhraní `10`. Číslo podrozhraní může být libovolné, ale je zvykem, že **odpovídá číslu VLAN**, aby se v konfiguraci nikdo nepletl. O skutečné VLAN rozhoduje jen `encapsulation dot1q`.

### Nativní VLAN na podrozhraní

Když přes trunk jde [[nativní VLAN]] bez tagu, router to musí vědět:

```
R1(config-subif)# encapsulation dot1q 99 native
```

### Stav podrozhraní

- podrozhraní je **up**, jen když je up fyzické rozhraní,
- `shutdown` na fyzickém rozhraní vypne všechna podrozhraní najednou,
- ověření: `show ip interface brief`, `show vlans`.

### Podrozhraní nejen pro VLAN

Podrozhraní se používají i na WAN linkách (Frame Relay, MPLS) nebo u [[ISP]], kde jeden fyzický port obsluhuje víc zákazníků.

**Souvisí:** [[Router-on-a-Stick]], [[Inter-VLAN routing]], [[802.1Q]], [[router]], [[VLAN]]
