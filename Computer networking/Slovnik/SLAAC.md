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

**Souvisí:** [[IPv6]], [[RA]], [[RS]], [[NDP]], [[EUI-64]], [[DAD]], [[LLA]], [[GUA]]
