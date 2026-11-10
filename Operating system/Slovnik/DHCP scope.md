---
aliases: [scope, DHCP obor, DHCP rozsah, DHCP options]
tags: [slovnik]
---

# DHCP scope

Rozsah IP adres, které [[DHCP]] server smí půjčovat v jedné síti, spolu s nastavením pro klienty. Např. scope `Ucebna` rozdává `192.168.16.100–200`.

---

## Podrobně

- **ScopeId** = adresa sítě (`192.168.16.0`), **maska**, **počáteční a koncová adresa**, **stav** (Active/Inactive)
- adresy mimo rozsah zůstávají pro zařízení s pevnou IP (brána, servery) → žádné konflikty
- **lease (zápůjčka)** – adresa se půjčuje na dobu, výchozí 8 dní (option 51 = 691200 s); klient ji průběžně obnovuje
- **options (volby)** posílané klientovi:
  - **003** Router – výchozí brána
  - **006** DNS Servers
  - **015** DNS Domain Name – přípona domény
- v doméně musí být DHCP server **autorizovaný v AD** (`Add-DhcpServerInDC`), jinak nic nerozdá – ochrana proti rogue DHCP
- příkazy: `Add-DhcpServerv4Scope`, `Set-DhcpServerv4OptionValue`, `Get-DhcpServerv4Lease`

**Souvisí:** [[02_DHCP]]
