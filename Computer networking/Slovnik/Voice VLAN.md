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

**Souvisí:** [[VLAN]], [[VoIP]], [[QoS]], [[Data VLAN]]
