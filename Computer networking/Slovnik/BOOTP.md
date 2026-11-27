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

### Jak probíhá

1. klient bez adresy pošle **BOOTREQUEST** jako [[broadcast]] (zná jen svou [[MAC adresa|MAC adresu]]),
2. server najde MAC v tabulce a pošle **BOOTREPLY** s IP adresou, adresou serveru a jménem souboru, ze kterého má klient nabootovat,
3. klient si soubor stáhne přes [[TFTP]].

### BOOTP vs. DHCP

| | BOOTP | [[DHCP]] |
| :-- | :-- | :-- |
| přidělení | jen statické (tabulka MAC → IP) | statické i dynamické |
| doba platnosti | napořád | zapůjčení na čas (lease) |
| další nastavení | málo | brána, DNS, doména a další |
| porty | UDP 67 / 68 | UDP 67 / 68 (stejné) |

### Kde se potkáš

- DHCP je s BOOTP zpětně kompatibilní, proto Wireshark ještě dlouho ukazoval DHCP zprávy pod názvem „Bootstrap Protocol",
- `ip helper-address` na routeru přeposílá BOOTP i DHCP,
- síťový start počítačů (PXE) dnes používá DHCP + TFTP, princip zůstal stejný.

**Souvisí:** [[DHCP]], [[UDP]]
