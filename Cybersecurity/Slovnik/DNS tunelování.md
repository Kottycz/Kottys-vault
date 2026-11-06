---
aliases: [DNS tunneling, DNS tunel, DNS exfiltrace]
tags: [slovnik]
---

# DNS tunelování

Schování dat nebo příkazů do **DNS dotazů na subdomény** – obchází firewall, protože DNS skoro nikdo neblokuje.

*Příklad: `ov5gs5tborswyplln52hi6j3nbsxg3.exfil-data.net` = zakódovaná data, ne skutečná subdoména.*

---

## Podrobně

- používá se pro **exfiltraci dat** a **C2** (řízení malwaru)
- data jsou zakódovaná (base32, base64, hex) v subdoméně
- znaky: **dlouhé** a divné dotazy, hodně dotazů na **jednu doménu**, typ TXT
- známé nástroje: **dnscat**, **dns2tcp**, iodine
- filtry: `dns.qry.name.len > 15 and !mdns`, `dns contains "dnscat"`

**Souvisí:** [[DNS]], [[ICMP tunelování]], [[Wireshark]]
