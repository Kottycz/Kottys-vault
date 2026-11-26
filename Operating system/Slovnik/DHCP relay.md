---
aliases: [DHCP relay agent, ip helper]
tags: [slovnik]
---

# DHCP relay

Zařízení (obvykle router), které přepošle [[DHCP]] **broadcast** z jedné sítě na [[DHCP]] server v jiné síti. Např. jeden [[DHCP]] server pro všechny učebny v různých VLAN.

---

## Podrobně

- broadcast router normálně nepropustí → bez relay klient v jiné síti [[DHCP]] server nenajde a dostane [[APIPA]]
- na Cisco routeru `ip helper-address`

**Souvisí:** [[DHCP]], [[02a_DHCP_teorie]]
