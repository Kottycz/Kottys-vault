---
aliases: [nslookup]
tags: [slovnik]
---

# nslookup

**nslookup** – příkaz, který se zeptá DNS serveru na IP adresu doménového jména.

*Příklad: `nslookup cisco.com` → vypíše IP adresu cisco.com a použitý DNS server.*

---

## Podrobně

- testuje, jestli funguje [[DNS]]
- typická situace z testu: **ping na IP funguje, ping na jméno ne** → problém s DNS → použij `nslookup`
- funguje ve Windows i Linuxu

| Příkaz (Windows) | K čemu |
| :-- | :-- |
| [[ipconfig]] | IP konfigurace počítače |
| [[ping]] | dostupnost zařízení |
| **nslookup** | překlad jména přes DNS |
| tracert ([[traceroute]]) | cesta paketu |

**Souvisí:** [[DNS]], [[ping]], [[ipconfig]]
