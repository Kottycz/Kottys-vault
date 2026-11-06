---
aliases: [reverzní DNS, reverzní vyhledávání DNS, reverse DNS]
tags: [slovnik]
---

# reverzní DNS

Převod **IP adresy na doménové jméno** (opak běžného [[DNS]]).

*Příklad: 93.184.216.34 → example.com.*

---

## Podrobně

- Nmap ho provádí jako krok skenování (po zjištění živých hostitelů)
- jména hostitelů mohou pentesterovi **prozradit informace** (např. `mail`, `vpn`, `db01`)
- `nmap -sL TARGETS` vypíše cíle a zkusí reverzní DNS u všech
- přepínač **`-n`** reverzní DNS vypne (méně provozu, rychlejší)
- přepínač **`-R`** vynutí reverzní DNS i pro **offline** hostitele
- **`--dns-servers DNS_SERVER`** určí vlastní DNS server
- výchozí chování: reverzní DNS jen pro **online** hostitele

**Souvisí:** [[DNS]], [[nmap]]
