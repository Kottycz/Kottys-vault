---
aliases: [Domain Name System]
tags: [slovnik]
---

# DNS

**Domain Name System** – systém doménových jmen. Překládá lidsky čitelné názvy (`seznam.cz`) na [[IP adresa|IP adresy]] (`77.75.79.222`). Port **53**, obvykle přes [[UDP]].

---

## Podrobně

### Proč existuje

Počítače komunikují přes IP adresy, lidé si ale pamatují jména. DNS je v podstatě "telefonní seznam internetu" – převádí jedno na druhé.

### Jak probíhá dotaz

Když zadáš `www.skola.cz`, počítač postupně ptá:

```
1. Lokální cache        → mám to už uložené?
2. Rekurzivní server    → (např. poskytovatele nebo 8.8.8.8)
3. Root server          → kdo spravuje .cz?
4. TLD server (.cz)     → kdo spravuje skola.cz?
5. Autoritativní server → jaká je IP www.skola.cz?
```

Odpověď se pak uloží do cache (na dobu danou **TTL**), aby se příště neptal znovu.

### Typy záznamů

| Typ | Význam |
| :-- | :-- |
| **A** | doména → [[IPv4]] adresa |
| **AAAA** | doména → [[IPv6]] adresa |
| **CNAME** | alias na jinou doménu |
| **MX** | mail server pro doménu (pro [[SMTP]]) |
| **NS** | který server je autoritativní |
| **PTR** | reverzní záznam (IP → doména) |
| **TXT** | libovolný text (ověřování domény, SPF) |

### Struktura domény

```
www  .  skola  .  cz  .
 |        |       |    |
 |        |       |    root (tečka, obvykle se nepíše)
 |        |       TLD (top-level domain)
 |        doména druhé úrovně
 subdoména
```

### Proč UDP

DNS dotaz i odpověď jsou malé a vejdou se do jednoho datagramu. Navazovat [[TCP]] spojení by trvalo déle než samotný dotaz. Když je odpověď příliš velká (nad 512 B), přepne se na TCP.

### Bezpečnost

Klasické DNS jde po síti nešifrovaně – kdokoliv vidí, na jaké weby se připojuješ, a útočník může odpověď podvrhnout. Řeší to **DNSSEC** (podepsané odpovědi), **DoH** (DNS over [[HTTPS]]) a **DoT** (DNS over TLS).

**Souvisí:** [[IP adresa]], [[UDP]], [[TTL]], [[DHCP]]
