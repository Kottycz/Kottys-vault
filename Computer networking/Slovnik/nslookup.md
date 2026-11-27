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

### Výstup

```
C:\> nslookup www.cisco.com
Server:  dns.google
Address: 8.8.8.8

Non-authoritative answer:
Name:    e2867.dsca.akamaiedge.net
Addresses:  2a02:26f0:…
          23.50.1.120
Aliases:  www.cisco.com
```

- **Server** – který DNS server odpověděl,
- **Non-authoritative answer** – odpověď je z cache, ne přímo od serveru, který doménu spravuje,
- **Aliases** – název je přezdívka (CNAME) pro jiný název.

### Užitečné varianty

| Příkaz | K čemu |
| :-- | :-- |
| `nslookup www.cisco.com 1.1.1.1` | zeptá se konkrétního DNS serveru |
| `nslookup -type=mx seznam.cz` | poštovní servery domény |
| `nslookup 8.8.8.8` | obrácený dotaz – jméno k IP adrese |

### Postup při problému „web nejde"

1. `ping 8.8.8.8` funguje → připojení k internetu je OK,
2. `ping www.google.com` nefunguje → problém je v DNS,
3. `nslookup www.google.com` → ukáže, jestli DNS server odpovídá a co vrací,
4. zkontrolovat DNS servery v `ipconfig /all`.

**Souvisí:** [[DNS]], [[ping]], [[ipconfig]]
