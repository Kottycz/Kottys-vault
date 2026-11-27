---
aliases: [L3 switch, Layer 3 switch, multilayer switch]
tags: [slovnik]
---

# přepínač vrstvy 3

**Přepínač vrstvy 3** (L3 switch) – [[switch]], který umí i **směrovat** mezi sítěmi, takže zvládne [[Inter-VLAN routing]] bez samostatného routeru. Příklad: pro každou VLAN má [[SVI]] s IP adresou.

---

## Podrobně

- zařízení vrstvy 3 pro směrování mezi VLAN, vedle [[router|routeru]],
- třetí možnost směrování mezi VLAN: přepínač vrstvy 3 využívající přepínaná virtuální rozhraní ([[SVI]]),
- host v jedné VLAN se bez routeru nebo přepínače vrstvy 3 nedostane do jiné VLAN.

### Konfigurace SVI pro směrování

```
S1(config)# ip routing
S1(config)# interface vlan 10
S1(config-if)# ip address 192.168.10.1 255.255.255.0
S1(config-if)# no shutdown
S1(config)# interface vlan 20
S1(config-if)# ip address 192.168.20.1 255.255.255.0
S1(config-if)# no shutdown
```

- `ip routing` zapne směrování, bez něj switch mezi VLAN nesměruje,
- každá VLAN má své [[SVI]] s IP adresou, ta je zároveň [[default gateway|bránou]] pro PC v té VLAN.

### Routed port

Port L3 switche se dá přepnout na „routovaný" port (jako port routeru), třeba pro spoj k routeru do internetu:

```
S1(config-if)# no switchport
S1(config-if)# ip address 10.0.0.1 255.255.255.252
```

### Proč je rychlejší než router

L3 switch směruje v **hardwaru** (speciální čipy ASIC), router z velké části v softwaru. Mezi VLAN v jedné budově proto L3 switch zvládne mnohem větší provoz.

### Ověření

`show ip route` (sítě VLAN jako připojené – C), `show ip interface brief` (SVI up/up).

**Souvisí:** [[switch]], [[SVI]], [[Inter-VLAN routing]], [[Router-on-a-Stick]], [[router]], [[VLAN]]
