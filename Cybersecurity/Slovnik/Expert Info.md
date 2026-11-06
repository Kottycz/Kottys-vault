---
aliases: [Expert Information, odborné informace]
tags: [slovnik]
---

# Expert Info

Přehled **varování a chyb**, které Wireshark sám našel v provozu – jen návrhy, ne jistota.

*Příklad: Warn: `Duplicate IP address configured (192.168.50.1)` = možný ARP poisoning.*

---

## Podrobně

- **Analyse → Expert Information** nebo ikona **vlevo dole** ve stavovém řádku
- závažnost: **Chat** (modrá), **Note** (tyrkysová), **Warn** (žlutá), **Error** (červená)
- skupiny: **Checksum**, **Comment**, **Deprecated**, **Malformed**, Sequence…
- může být falešně pozitivní/negativní – Wireshark **není [[IDS]]**

**Souvisí:** [[Wireshark]], [[ARP poisoning]], [[IDS]]
