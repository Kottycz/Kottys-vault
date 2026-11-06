---
aliases: [ARP spoofing, ARP otrava, MITM, Man In The Middle]
tags: [slovnik]
---

# ARP poisoning

Útok, kdy útočník posílá **falešné ARP odpovědi** a přesměruje provoz oběti přes sebe (Man In The Middle).

*Příklad: útočník tvrdí „`192.168.1.1` je na mé MAC" → oběť posílá data pro bránu jemu.*

---

## Podrobně

- [[ARP]] nemá ověřování → kdokoli může tvrdit, že má libovolnou IP
- typicky se útočník vydává za **bránu** (vůči oběti) a za **oběť** (vůči bráně)
- znaky ve Wiresharku:
  - dvě různé MAC pro jednu IP → Expert Info `Duplicate IP address`
  - záplava ARP requestů od jedné MAC (ARP scan)
  - HTTP pakety oběti mají **cílovou MAC útočníka**
- filtry: `arp.duplicate-address-detected or arp.duplicate-address-frame`, `arp.opcode == 2`
- tip: **Apply as Column** na `eth.src` / `eth.dst`

**Souvisí:** [[ARP]], [[Wireshark]], [[MAC spoofing]], [[IP spoofing]]
