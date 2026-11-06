---
aliases: [Wireshark, tcpdump]
tags: [slovnik]
---

# Wireshark

Program, který **zachytává a zobrazuje síťový provoz** paket po paketu.

*Příklad: s filtrem `arp` ukáže všechny dotazy `Who has 10.10.210.1? Tell 10.10.210.6`.*

---

## Podrobně

- sloupce: **Source, Destination, Protocol, Info**
- **filtry** zobrazení: `arp`, `icmp`
- umožňuje vidět, co přesně skener posílá po síti
- podobný nástroj bez grafického rozhraní: **tcpdump**
- typ [[sniffer|snifferu]] – analyzátoru protokolů

| Sken | Co ve Wiresharku vidím |
| :-- | :-- |
| `nmap -PR -sn` | ARP broadcast `Who has ...?` na každou IP |
| `nmap -PE -sn` | `Echo (ping) request` |
| `nmap -PP -sn` | `Timestamp request` |
| `nmap -PM -sn` | `Address mask request` (každý dvakrát) |

Zápisy: [[01_Wireshark_Basics|Basics]] · [[02_Wireshark_Packet_Operations|Packet Operations]] · [[03_Wireshark_Traffic_Analysis|Traffic Analysis]] · [[04_Wireshark_Video_Mastering|Video]] · [[Wireshark souhrn]] · [[Wireshark příkazy]] · [[Wireshark cvičení]]

**Souvisí:** [[sniffer]], [[ARP]], [[ICMP]], [[nmap]], [[PCAP]], [[capture filter]], [[display filter]], [[Follow Stream]], [[Expert Info]]
