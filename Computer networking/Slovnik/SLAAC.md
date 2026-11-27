---
aliases: [Stateless Address Autoconfiguration, bezstavová autokonfigurace]
tags: [slovnik]
---

# SLAAC

**Stateless Address Autoconfiguration** – způsob, jakým si zařízení v [[IPv6]] **samo vytvoří adresu** z informací od [[router|routeru]], bez DHCP serveru.

---

## Podrobně

### Průběh

1. Zařízení si vytvoří [[LLA]] (`fe80::...`)
2. Ověří přes [[DAD]], že ji nikdo nemá
3. Pošle [[RS]] (Router Solicitation) – „je tu nějaký router?"
4. Router odpoví [[RA]] (Router Advertisement) s prefixem sítě
5. Zařízení spojí prefix z RA se svým ID rozhraní → `2001:db8:acad:1::` + `...:f156`
6. Znovu ověří přes DAD a adresu použije

Router zároveň v RA pošle svoji [[LLA]] jako [[default gateway]].

### Odkud se bere ID rozhraní

- **[[EUI-64]]** – odvozeno z [[MAC adresa|MAC adresy]] (nevýhoda: adresa prozrazuje hardware a dá se sledovat)
- **Náhodné** – dnes běžnější, kvůli soukromí (privacy extensions), občas se mění

### Tři režimy podle RA

Router v RA nastaví příznaky, které určí, co má zařízení udělat:

| Režim | Adresa | Ostatní údaje (DNS…) |
| :-- | :-- | :-- |
| **SLAAC** | vytvoří si sám | z RA |
| **Stateless DHCPv6** | vytvoří si sám | z DHCPv6 serveru |
| **Stateful DHCPv6** | přidělí DHCPv6 | z DHCPv6 |

### SLAAC vs. DHCP

| | SLAAC | [[DHCP]]v6 |
| :-- | :-- | :-- |
| Server potřeba | ne | ano |
| Kdo drží evidenci | nikdo (bezstavové) | server (stavové) |
| Přehled o zařízeních | ne | ano |
| Nastavení navíc | omezené | plné |

Proto se ve firmách často používá DHCPv6 (kvůli evidenci), doma stačí SLAAC.

### Podmínka

SLAAC vyžaduje **prefix /64** – zbylých 64 bitů musí zbýt na ID rozhraní.

### Ukázka – co si PC vytvoří

Router posílá RA s prefixem `2001:db8:acad:1::/64`. PC si vytvoří:

```
2001:db8:acad:1:a1b2:c3d4:e5f6:7890   ← GUA (prefix + náhodné ID)
fe80::a1b2:c3d4:e5f6:7890             ← LLA
```

Výchozí bránou bude **link-local adresa routeru** (zdrojová adresa RA), ne jeho GUA.

### Dočasné adresy

Windows si kromě stálé adresy vytváří i **dočasné** (temporary) adresy, které se pravidelně mění. Pro odchozí spojení se používají ty, aby se uživatel nedal sledovat podle stálé adresy. V `ipconfig` je uvidíš jako „Temporary IPv6 Address".

### Ověření

| Kde | Příkaz |
| :-- | :-- |
| Windows | `ipconfig` (IPv6 adresa, Default Gateway `fe80::…`) |
| Cisco router | `show ipv6 interface g0/0/0` (posílá RA?) |
| Cisco – kdo je v síti | `show ipv6 neighbors` |

**Souvisí:** [[IPv6]], [[RA]], [[RS]], [[NDP]], [[EUI-64]], [[DAD]], [[LLA]], [[GUA]]
