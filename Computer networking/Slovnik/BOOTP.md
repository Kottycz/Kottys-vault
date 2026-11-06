---
aliases: [BOOTP, Bootstrap Protocol]
tags: [slovnik]
---

# BOOTP

**BOOTP (Bootstrap Protocol)** – starší protokol, přes který si **bezdiskový počítač** zjistí svou IP adresu a adresu serveru, ze kterého nabootuje.

*Příklad: stanice bez disku se po zapnutí zeptá BOOTP serveru na IP a na server se systémem.*

---

## Podrobně

- předchůdce [[DHCP]]
- používá UDP porty **67 (server)** a **68 (klient)** – stejné jako DHCP
- adresy přiděluje **staticky** podle tabulky (MAC → IP), DHCP umí i dynamicky a na dobu pronájmu

**Souvisí:** [[DHCP]], [[UDP]]
