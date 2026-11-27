---
aliases: [router on a stick, ROAS, router-on-a-stick]
tags: [slovnik]
---

# Router-on-a-Stick

**Router-on-a-Stick** – způsob směrování mezi [[VLAN]], kdy je s přepínačem spojený **jen jeden fyzický kabel** (trunk) a na routeru je pro každou VLAN jedno [[subinterface|podrozhraní]]. Příklad: `G0/0/1.10` pro VLAN 10 a `G0/0/1.20` pro VLAN 20.

---

## Podrobně

- vyžaduje pouze jedno fyzické [[Ethernet|ethernetové]] rozhraní,
- rozhraní routeru Cisco [[IOS]] je nastavené jako trunk [[802.1Q]] a připojené k trunk portu na přepínači vrstvy 2,
- tagovaný rámec VLAN přijme podrozhraní **zdrojové VLAN** podle tagu,
- router paket směruje podle **cílové IP adresy** a odešle ho přes podrozhraní **cílové VLAN** s novým tagem,
- fyzické rozhraní se aktivuje jednou (`no shutdown`), podrozhraní se konfigurují zvlášť.

### Celá konfigurace (příklad)

Switch – port do routeru jako trunk:

```
S1(config)# interface g0/1
S1(config-if)# switchport mode trunk
```

Router – podrozhraní pro VLAN 10, 20 a management VLAN 99:

```
R1(config)# interface g0/0/1.10
R1(config-subif)# encapsulation dot1q 10
R1(config-subif)# ip address 192.168.10.1 255.255.255.0
R1(config)# interface g0/0/1.20
R1(config-subif)# encapsulation dot1q 20
R1(config-subif)# ip address 192.168.20.1 255.255.255.0
R1(config)# interface g0/0/1.99
R1(config-subif)# encapsulation dot1q 99
R1(config-subif)# ip address 192.168.99.1 255.255.255.0
R1(config)# interface g0/0/1
R1(config-if)# no shutdown
```

PC ve VLAN 10 mají bránu `192.168.10.1`, ve VLAN 20 `192.168.20.1`.

### Ověření

| Příkaz | Co hledat |
| :-- | :-- |
| `show ip interface brief` | podrozhraní up/up |
| `show ip route` | sítě všech VLAN jako C (připojené) |
| `show vlans` (na routeru) | které VLAN jsou na kterém podrozhraní |
| `show interfaces trunk` (na switchi) | port do routeru je trunk, VLAN jsou povolené |

### Nevýhoda

Všechen provoz mezi VLAN jde **tam a zpátky po jednom kabelu**. Při velkém provozu se linka stane úzkým hrdlem a router je [[single point of failure]].

**Souvisí:** [[Inter-VLAN routing]], [[subinterface]], [[VLAN trunk]], [[802.1Q]], [[router]]
