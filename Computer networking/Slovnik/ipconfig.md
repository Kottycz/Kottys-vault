---
aliases: [ipconfig /all, ipconfig /release, ipconfig /renew, arp -a]
tags: [slovnik]
---

# ipconfig

**Příkaz Windows, který zobrazí a ovládá síťové nastavení hostitele** – IP adresu, masku, bránu a další.

```
ipconfig /all
```

---

## Podrobně

### Varianty z učiva

| Příkaz | Co dělá |
| :-- | :-- |
| `ipconfig` | základní přehled ([[IP adresa]], [[maska podsítě]], [[default gateway]]) |
| `ipconfig /all` | **kompletní** nastavení – [[MAC adresa]], [[DNS]] servery, informace o [[DHCP]] |
| `ipconfig /release` | **uvolní** adresu získanou od DHCP serveru |
| `ipconfig /renew` | **požádá** DHCP server o novou nebo obnovenou adresu |

### Release + renew

Používá se, když počítač dostal špatnou adresu nebo se změnila síť:

```
ipconfig /release
ipconfig /renew
```

Počítač si nejdřív vrátí starou adresu a pak si znovu vyžádá novou (viz [[DORA]]).

### arp -a

Spolu s ipconfig se v učivu uvádí **`arp -a`** – vypíše [[ARP]] tabulku hostitele (naučené dvojice IP ↔ MAC).

### Na jiných systémech

Na Linuxu a macOS se používá `ip addr` (nebo starší `ifconfig`).

### Výstup ipconfig /all

| Řádek | Co znamená |
| :-- | :-- |
| Physical Address | [[MAC adresa]] karty |
| DHCP Enabled | jestli adresu přiděluje [[DHCP]] |
| IPv4 Address | IP adresa (s „Preferred") |
| Subnet Mask | [[maska podsítě]] |
| Default Gateway | [[default gateway|výchozí brána]] |
| DHCP Server | kdo adresu přidělil |
| DNS Servers | které [[DNS]] servery se používají |
| Lease Obtained / Expires | kdy byla adresa přidělena a kdy vyprší |

### Rychlá diagnostika

| Vidíš | Znamená |
| :-- | :-- |
| `169.254.x.x` | DHCP neodpověděl (APIPA) |
| chybí Default Gateway | nedostaneš se mimo svou síť |
| `Media disconnected` | odpojený kabel nebo Wi-Fi |

### Další příkazy

- `ipconfig /flushdns` – smaže DNS cache,
- `ipconfig /displaydns` – ukáže DNS cache.

**Souvisí:** [[IP adresa]], [[DHCP]], [[ARP]], [[ping]], [[příkazy show]], [[Budovani_male_site]]
