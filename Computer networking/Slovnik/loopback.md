---
aliases: [localhost, smyčka, 127.0.0.1]
tags: [slovnik]
---

# loopback

**Adresa, kterou zařízení oslovuje samo sebe.** U [[IPv4]] je to `127.0.0.1`, u [[IPv6]] `::1`. Provoz na ni nikdy neopustí zařízení.

---

## Podrobně

### Rozsah

| Verze | Adresa / rozsah |
| :-- | :-- |
| [[IPv4]] | `127.0.0.0/8` (nejčastěji `127.0.0.1`) |
| [[IPv6]] | `::1` |

Celý blok 127.x.x.x je vyhrazen – funguje i `127.0.0.5`, ale zvykem je první adresa. Jménem se jí říká **localhost**.

### K čemu slouží

- **Test TCP/IP stacku** – `ping 127.0.0.1` ověří, že síťová část systému funguje, i když není zapojený kabel
- **Lokální vývoj** – webový server běží na `http://localhost:8080`, dostupný jen z toho počítače
- **Komunikace mezi procesy** na jednom stroji

### První krok při hledání problému

1. `ping 127.0.0.1` – funguje můj TCP/IP stack?
2. `ping` na vlastní IP – je v pořádku moje [[NIC|síťovka]]?
3. `ping` na [[default gateway|výchozí bránu]] – vidím router?
4. `ping 8.8.8.8` – mám internet?
5. `ping seznam.cz` – funguje [[DNS]]?

### Loopback rozhraní na routeru

Na Cisco zařízeních se dá vytvořit i **virtuální loopback rozhraní** s vlastní IP adresou:

```
Router(config)# interface loopback 0
Router(config-if)# ip address 1.1.1.1 255.255.255.255
```

Na rozdíl od fyzického portu **nikdy nespadne** – proto se používá jako stabilní identifikátor routeru ve směrovacích protokolech ([[OSPF]], [[BGP]]) a pro správu.

**Souvisí:** [[IPv4]], [[IPv6]], [[ping]], [[IP adresa]], [[OSPF]], [[default gateway]]
