---
aliases: [promiscuous mode, promisc]
tags: [slovnik]
---

# promiskuitní režim

Režim síťové karty, kdy **přijímá všechny pakety**, které vidí – i ty, co nejsou určené jí.

*Příklad: bez něj Wireshark na switchi zachytí jen provoz vlastního počítače a broadcasty.*

---

## Podrobně

- normálně karta zahodí rámce s cizí cílovou MAC
- v promiskuitním režimu je předá systému → [[Wireshark]] je zachytí
- zapíná se v **Capture Options** (`Ctrl+K`) u rozhraní
- na Wi-Fi existuje ještě **monitor mode** (zachytí i provoz cizích sítí)
- důvod, proč někdy nevidím pakety: provoz neexistuje, není pro mě, nebo je vypnutý promiskuitní režim

**Souvisí:** [[Wireshark]], [[sniffer]]
