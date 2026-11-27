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

### Konfigurace

```
S1(config)# vlan 99
S1(config-vlan)# name Management
S1(config)# interface vlan 99
S1(config-if)# ip address 192.168.99.11 255.255.255.0
S1(config-if)# no shutdown
S1(config)# ip default-gateway 192.168.99.1
```

- SVI `interface vlan 99` dostane IP adresu, přes kterou se ke switchi připojíš,
- `ip default-gateway` je nutná, abys switch spravoval i z jiné sítě,
- SVI je **up/up**, jen když existuje VLAN 99 a aspoň jeden port v ní (nebo trunk, který ji nese) je aktivní.

### Bezpečnost správy

- v Management VLAN jen admini a síťová zařízení, ne uživatelé,
- přístup jen přes [[SSH]], [[Telnet]] vypnout,
- na VTY linkách ACL, které pustí jen adresy adminů.

### Ověření

`show ip interface brief` (stav SVI), `show vlan brief`, pak ze PC admina `ssh` na IP switche.

**Souvisí:** [[VLAN]], [[SVI]], [[Default VLAN]], [[SSH]], [[Telnet]]
