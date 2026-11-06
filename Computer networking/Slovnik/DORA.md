---
aliases: [Discover Offer Request Acknowledge]
tags: [slovnik]
---

# DORA

**Discover – Offer – Request – Acknowledge** – čtyři kroky, kterými [[DHCP]] přiděluje zařízení [[IP adresa|IP adresu]].

---

## Podrobně

### Čtyři kroky

| # | Krok | Kdo | Co říká |
| :-- | :-- | :-- | :-- |
| 1 | **DISCOVER** | klient ([[broadcast]]) | „je tu nějaký DHCP server? Potřebuju adresu" |
| 2 | **OFFER** | server | „nabízím ti 192.168.1.50, maska /24, brána .1, [[DNS]] 8.8.8.8, na 24 hodin" |
| 3 | **REQUEST** | klient (broadcast) | „beru si tu adresu od tohoto serveru" |
| 4 | **ACK** | server | „potvrzeno, je tvoje" |

### Proč broadcast

V kroku 1 klient **ještě nemá žádnou adresu** ani neví, kde je server – musí se tedy ptát všech (`255.255.255.255`).

Krok 3 je taky [[broadcast]], i když už adresu zná – aby ostatní DHCP servery, které taky nabízely, věděly, že jejich nabídka nebyla přijata a mohly adresu vrátit do fondu.

### Co se přidělí

Adresa, [[maska podsítě]], [[default gateway]], [[DNS]] servery, doba zapůjčení (lease), případně další.

### Obnovení zapůjčení

V polovině doby lease se klient pokusí adresu obnovit – pošle rovnou **REQUEST** (už ne DISCOVER) přímo serveru. Ten odpoví **[[ACK]]** a lease se prodlouží. Celé DORA tedy probíhá jen při prvním připojení.

### DHCP Relay

DHCP jede přes broadcast, který [[router]] nepropustí. Když je server v jiné podsíti, nastaví se na routeru **DHCP relay** (`ip helper-address`) – ten broadcast zachytí a přepošle serveru jako [[unicast]].

**Souvisí:** [[DHCP]], [[broadcast]], [[IP adresa]], [[default gateway]], [[maska podsítě]], [[ACK]]
