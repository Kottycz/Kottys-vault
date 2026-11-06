---
aliases: [pcap, pcapng, .pcap, .pcapng, packet capture]
tags: [slovnik]
---

# PCAP

Soubor se **zachyceným síťovým provozem** – paket po paketu, aby se dal později analyzovat.

*Příklad: `Exercise.pcapng` otevřený ve Wiresharku přes File → Open.*

---

## Podrobně

- **PCAP** = Packet CAPture
- `.pcap` – starší formát (libpcap), umí i tcpdump
- `.pcapng` – novější, **výchozí ve Wiresharku**; umí **komentáře** k souboru i k paketům, víc rozhraní
- vytváří ho [[Wireshark]], tcpdump, TShark…
- detaily souboru: **Statistics → Capture File Properties** (hash, čas, počet paketů)
- víc souborů jde spojit: **File → Merge**

**Souvisí:** [[Wireshark]], [[capture filter]], [[display filter]]
