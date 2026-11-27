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

### Jak router rozhoduje

1. přijme rámec, zkontroluje [[FCS]] a vybalí paket,
2. sníží [[TTL]] o 1 (když je 0, paket zahodí a pošle ICMP time exceeded),
3. hledá cílovou IP ve [[směrovací tabulka|směrovací tabulce]] – vybere **nejdelší shodu** prefixu,
4. když shodu nenajde a nemá výchozí cestu, paket zahodí,
5. zabalí paket do nového rámce pro výstupní rozhraní (nové MAC adresy) a pošle.

### Zdroje cest

| Kód v `show ip route` | Zdroj | AD |
| :-- | :-- | :-- |
| C | přímo připojená síť | 0 |
| L | vlastní adresa rozhraní (local) | 0 |
| S | statická cesta | 1 |
| D | [[EIGRP]] | 90 |
| O | [[OSPF]] | 110 |
| R | RIP | 120 |

### Základní konfigurace

```
Router(config)# hostname R1
R1(config)# enable secret Cisco123
R1(config)# interface g0/0/0
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# description LAN
R1(config-if)# no shutdown
```

Rozhraní routeru jsou ve výchozím stavu **vypnutá** (na rozdíl od switche), proto je potřeba `no shutdown`.

**Souvisí:** [[switch]], [[IP adresa]], [[default gateway]], [[OSPF]], [[NAT]], [[TTL]], [[broadcast]]
