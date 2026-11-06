---
aliases: [směrovač, routery]
tags: [slovnik]
---

# router

**Směrovač** – zařízení síťové vrstvy (OSI 3), které propojuje **různé sítě** a rozhoduje, kudy poslat paket k cíli podle [[IP adresa|IP adresy]].

---

## Podrobně

### Co dělá

1. Přijme rámec, rozbalí z něj paket
2. Podívá se na cílovou IP adresu
3. Najde ve **směrovací tabulce**, kudy vede cesta
4. Zabalí paket do nového rámce (s novými MAC adresami) a pošle dál

Každý průchod routerem = jeden **hop**. Router přitom sníží [[TTL]] o 1 – když dosáhne nuly, paket zahodí (ochrana proti smyčkám).

### Směrovací tabulka

Obsahuje záznamy typu "pro síť X pošli paket na rozhraní Y / další router Z". Zdroje záznamů:

- **Přímo připojené sítě** – automaticky podle nastavených rozhraní
- **Statické routy** – nastavené ručně správcem
- **Dynamické routy** – naučené směrovacím protokolem ([[OSPF]], [[EIGRP]], [[BGP]])

Zobrazení: `show ip route` (Cisco)

### Router vs. switch

| | router | [[switch]] |
| :-- | :-- | :-- |
| Vrstva OSI | 3 (síťová) | 2 (spojová) |
| Adresuje podle | [[IP adresa\|IP adresy]] | [[MAC adresa\|MAC adresy]] |
| Propojuje | různé sítě | zařízení v jedné síti |
| [[broadcast]] | zastaví ho | přepošle ho |

Switch tvoří jednu broadcastovou doménu, router ji **rozděluje** – to je jeho klíčová vlastnost.

### Domácí "router"

Krabička od poskytovatele obvykle kombinuje víc zařízení: router + switch + Wi-Fi přístupový bod ([[AP]]) + [[NAT]] + [[DHCP]] server + [[firewall]].

### Rozhraní

- **LAN porty** – do vnitřní sítě
- **WAN port** – k poskytovateli ([[ISP]])
- Každé rozhraní má vlastní IP adresu a je v jiné síti

**Souvisí:** [[switch]], [[IP adresa]], [[default gateway]], [[OSPF]], [[NAT]], [[TTL]], [[broadcast]]
