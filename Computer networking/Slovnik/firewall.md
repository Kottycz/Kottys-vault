---
aliases: [brána firewall]
tags: [slovnik]
---

# firewall

**Zařízení nebo software, který filtruje síťový provoz** podle daných pravidel. Blokuje nežádoucí komunikaci mezi sítěmi.

---

## Podrobně

### Podle čeho filtruje

- Zdrojová a cílová [[IP adresa]]
- Zdrojový a cílový [[port]]
- Protokol ([[TCP]], [[UDP]], [[ICMP]])
- Směr provozu (dovnitř / ven)
- U pokročilých i konkrétní aplikace nebo obsah

### Typy

| Typ | Popis |
| :-- | :-- |
| **Paketový filtr** | rozhoduje o každém paketu zvlášť podle hlavičky (jednoduchý, rychlý) |
| **Stavový (stateful)** | sleduje celá spojení – propustí odpověď na provoz, který sám vypustil ven |
| **Aplikační / NGFW** | rozumí obsahu, umí filtrovat konkrétní aplikace, obsahuje IPS a antivirus |

### Kde bývá

- **Hostitelský firewall** – na počítači (Windows Defender Firewall), chrání jedno zařízení
- **Síťový firewall** – na hranici sítě, chrání celou [[LAN]]
- **V domácím [[router|routeru]]** – základní filtrování, často spojené s [[NAT]]

### Výchozí pravidlo

Bezpečný firewall funguje na principu **"co není výslovně povoleno, je zakázáno"** (default deny). Opačný přístup (default allow) znamená, že stačí zapomenout na jedno pravidlo a díra je otevřená.

### DMZ

Oddělená zóna pro servery dostupné z internetu (web, mail). Když někdo napadne server v DMZ, nedostane se tím do vnitřní sítě – ta je za dalším firewallem.

### Související prvky

- **IDS** – detekuje útoky a hlásí je
- **IPS** – detekuje a rovnou blokuje
- **Proxy** – zprostředkovává spojení, umí filtrovat obsah

**Souvisí:** [[NAT]], [[router]], [[port]], [[IP adresa]], [[VPN]]
