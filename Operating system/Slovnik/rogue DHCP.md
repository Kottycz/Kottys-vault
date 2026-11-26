---
aliases: [falešný DHCP server]
tags: [slovnik]
---

# rogue DHCP

Neautorizovaný [[DHCP]] server v síti, který klientům rozdává špatné údaje (bránu, [[DNS]]) a může přesměrovat jejich provoz. Např. domácí router zapojený do učebny.

---

## Podrobně

- klient bere **první** nabídku, která dorazí
- ochrana ve Windows doméně: [[DHCP]] server musí být **autorizovaný v [[AD DS|AD]]** (`Add-DhcpServerInDC`)

**Souvisí:** [[DHCP scope]], [[02a_DHCP_teorie]]
