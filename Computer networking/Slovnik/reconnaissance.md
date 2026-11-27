---
aliases: [reconnaissance, průzkum, průzkumný útok]
tags: [slovnik]
---

# reconnaissance

**Reconnaissance (průzkum)** – útok, při kterém útočník sbírá informace o síti, aby později mohl zaútočit.

*Příklad: útočník u budovy skenuje WiFi sítě a zjišťuje jejich názvy a zabezpečení.*

---

## Podrobně

- první fáze útoku – útočník zatím nic neničí
- zjišťuje: IP adresy, otevřené porty, běžící služby, typy zařízení, WiFi sítě
- nástroje: ping sweep, skenery portů, dotazy na [[DNS]], `whois`
- typy síťových útoků v CCNA:

| Útok | Co dělá |
| :-- | :-- |
| **reconnaissance** | sběr informací |
| **access** | získání přístupu (hesla, [[MITM]]) |
| **DoS** | zahlcení služby ([[DoS-DDoS]]) |

### Nástroje a metody

| Metoda | Co útočník zjistí |
| :-- | :-- |
| dotazy na internetu (whois, DNS) | adresy, jména serverů, kontakty |
| ping sweep | které IP adresy jsou živé |
| sken portů | jaké služby na zařízení běží |
| zjištění verze služeb | zranitelné verze softwaru |
| sociální inženýrství | jména, struktura firmy |

### Obrana

- blokovat zbytečné ICMP z internetu na hranici sítě,
- zavřít nepoužívané porty a vypnout nepotřebné služby,
- neukazovat verze softwaru v bannerech,
- [[IPS]], který rozpozná skenování,
- logovat a sledovat neobvyklé dotazy.

### Fáze útoku

Průzkum → získání přístupu → udržení přístupu → útok (krádež dat, [[DoS-DDoS|DoS]]). Kdo zachytí průzkum, může útok zastavit dřív, než začne.

**Souvisí:** [[DoS-DDoS]], [[MITM]], [[brute force]]
