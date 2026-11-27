---
aliases: [hlasová VLAN]
tags: [slovnik]
---

# Voice VLAN

**Voice VLAN** – samostatná [[VLAN]] pro hlasový provoz ([[VoIP]]), aby hovory nebyly rušené běžnými daty. Příklad: IP telefon na stole je ve voice VLAN, PC za ním v datové.

---

## Podrobně

- VoIP potřebuje zaručenou šířku pásma a vysokou prioritu ([[QoS]]),
- proto je oddělená od [[Data VLAN|datových]] VLAN,
- port switche, ke kterému je připojený IP telefon, je výjimka: smí patřit do více než jedné VLAN (data + voice).

### Konfigurace

```
S1(config)# vlan 150
S1(config-vlan)# name Hlas
S1(config)# interface fa0/18
S1(config-if)# switchport mode access
S1(config-if)# switchport access vlan 20
S1(config-if)# mls qos trust cos
S1(config-if)# switchport voice vlan 150
```

- `access vlan 20` – data z PC za telefonem,
- `voice vlan 150` – hlas z telefonu,
- `mls qos trust cos` – switch věří prioritě, kterou nastaví telefon.

### Jak to funguje

IP telefon má v sobě malý switch. PC se zapojí do telefonu, telefon do switche. Switch telefonu přes [[CDP]] řekne číslo voice VLAN. Telefon pak svůj hlas posílá s tagem voice VLAN (a vysokou prioritou), data z PC bez tagu do access VLAN.

### Ověření

`show interfaces fa0/18 switchport` – řádky „Access Mode VLAN" a „Voice VLAN".

**Souvisí:** [[VLAN]], [[VoIP]], [[QoS]], [[Data VLAN]]
