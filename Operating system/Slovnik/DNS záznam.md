---
aliases: [A záznam, PTR, CNAME, DNS zóna, reverzní zóna, resource record]
tags: [slovnik]
---

# DNS záznam

Řádek v **zóně** [[DNS]] serveru, který říká, kam jméno (nebo IP) vede. Např. A záznam `srv2-fs → 192.168.16.20`.

---

## Podrobně

### Zóny

- **dopředná (forward)** – jméno → IP, např. `kotrba.cyberschool.internal`
- **reverzní (reverse)** – IP → jméno, jméno zóny je síť pozpátku + `in-addr.arpa`, např. `16.168.192.in-addr.arpa`; nevzniká sama
- **AD-integrovaná** – uložená v Active Directory, replikuje se s ní, umí **Secure** dynamické aktualizace (zapisovat smí jen členové domény)

### Typy záznamů

| Typ | Význam | Příklad |
| :-- | :-- | :-- |
| **A** | jméno → IPv4 | `srv1-dc → 192.168.16.10` |
| **AAAA** | jméno → IPv6 | |
| **PTR** | IP → jméno (v reverzní zóně) | `10 → srv1-dc.kotrba.cyberschool.internal` |
| **CNAME** | alias → jiné jméno | `ftp → srv2-fs.kotrba.cyberschool.internal` |
| **SRV** | kde běží služba (např. řadič domény) | v zóně `_msdcs` |
| **NS / SOA** | kdo je autoritou pro zónu | |
| **MX** | poštovní server domény (s prioritou) | `frengp.cz MX 10 mail.frengp.cz` |
| **TXT** | libovolný text – ověření domény, [[SPF-DKIM-DMARC\|SPF, DKIM, DMARC]] | |
| **CAA** | která [[CA]] smí vydat certifikát | |

- dynamicky se zapisují klienti sami (`ipconfig /registerdns`), statické záznamy zakládá správce (`Add-DnsServerResourceRecordA ... -CreatePtr`)

**Souvisí:** [[reverzní DNS]], [[03_DNS]]
