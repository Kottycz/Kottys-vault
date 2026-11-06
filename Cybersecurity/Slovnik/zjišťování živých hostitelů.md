---
aliases: [live host discovery, živý hostitel, zjišťování živých hostitelů, host discovery]
tags: [slovnik]
---

# zjišťování živých hostitelů

**Live host discovery** – první fáze skenování: zjistit, **které systémy v síti jsou online**, než se na ně pustí skenování portů.

*Příklad: z 254 adres v podsíti odpoví jen 12 → porty se skenují jen na nich.*

---

## Podrobně

**Proč:** skenování portů na vypnutém systému ztrácí čas a dělá v síti zbytečný šum.

| Metoda | Vrstva | Jak funguje |
| :-- | :-- | :-- |
| **[[ARP]] scan** | linková | ARP request na broadcast; odpověď = host je online. Funguje jen ve **stejné podsíti** |
| **[[ICMP]] ping** | síťová | Echo (Type 8) → Echo Reply (Type 0). Může ho blokovat [[firewall]] |
| **TCP ping** | transportní | paket na běžný port [[TCP]]; odpověď = host žije |
| **UDP ping** | transportní | paket na běžný port [[UDP]]; účinné, když je ICMP blokované |

- ICMP má tři varianty: echo (`-PE`), [[ICMP timestamp|timestamp]] (`-PP`), [[ICMP address mask|address mask]] (`-PM`); jen zjišťování bez portů = [[ping scan]] (`-sn`)
- ARP se **nesměruje** – pro jinou podsíť je potřeba ICMP nebo TCP/UDP
- související nástroje: [[arp-scan]], [[masscan]], [[nmap|Nmap]]

**Souvisí:** [[nmap]], [[arp-scan]], [[masscan]], [[ping]], [[ARP]], [[ICMP]]
