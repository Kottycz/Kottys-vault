---
aliases: [arp-scan]
tags: [slovnik]
---

# arp-scan

Nástroj, který zjišťuje živé hostitele v lokální síti pomocí dotazů [[ARP]].

*Příklad: najde všechna zařízení v domácí síti i s jejich MAC adresami.*

---

## Podrobně

- pracuje na **linkové vrstvě**, takže funguje jen ve **stejné podsíti** (ARP se nesměruje)
- výhoda: ARP se těžko blokuje a odpoví skoro každé zařízení
- v místnosti se probírá, jak se překrývá s [[zjišťování živých hostitelů|zjišťováním hostitelů]] v [[nmap|Nmapu]]
- není na AttackBoxu: `apt install arp-scan`

| Příkaz | Co dělá |
| :-- | :-- |
| `arp-scan -l` / `--localnet` | ARP dotazy na všechny platné IP ve všech lokálních sítích |
| `arp-scan -I eth0 -l` | jen na rozhraní eth0 |
| `arp-scan 10.10.210.6/24` | zadaná podsíť |

Výsledek: 256 hostitelů za 2,7 s, 3 odpověděli – stejně jako `nmap -PR -sn`. V [[Wireshark|Wiresharku]] jsou pakety podobné.

**Souvisí:** [[ARP]], [[masscan]], [[nmap]], [[zjišťování živých hostitelů]]
