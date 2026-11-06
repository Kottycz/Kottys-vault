---
aliases: [IP address, IP adresy]
tags: [slovnik]
---

# IP adresa

**Logická adresa síťové vrstvy** (OSI 3), která identifikuje zařízení i síť, ve které se nachází. Slouží k doručení paketu od původního zdroje ke konečnému cíli.

---

## Podrobně

### Dvě části každé adresy

| Část | [[IPv4]] | [[IPv6]] |
| :-- | :-- | :-- |
| Označuje síť | síťová část | prefix |
| Označuje zařízení | hostitelská část | ID rozhraní |

Kde přesně je hranice, určuje [[maska podsítě]] (IPv4) nebo [[délka prefixu]] (IPv6). Všechna zařízení ve stejné síti mají **shodnou síťovou část**.

### Verze

- **IPv4** – 32 bitů, `192.168.1.10`
- **IPv6** – 128 bitů, `2001:db8::1`

### Veřejná vs. privátní

- **Veřejná** – jedinečná na celém internetu, směrovatelná
- **Privátní** – jen pro vnitřní sítě (10.x, 172.16–31.x, 192.168.x), na internet se dostane až přes [[NAT]]

### Statická vs. dynamická

- **Statická** – nastavená ručně, nemění se (servery, tiskárny, síťové prvky)
- **Dynamická** – přidělená z [[DHCP]] (běžná zařízení)

### IP vs. MAC

[[MAC adresa]] je fyzická, platí jen v rámci jedné sítě a nemění se. IP adresa je logická, platí globálně a mění se podle toho, kde je zařízení připojené. Při cestě paketu sítí se **MAC adresy přepisují na každém [[router|routeru]], IP adresy zůstávají**.

### Příklad cesty

| Situace | Zdroj | Cíl | Jak |
| :-- | :-- | :-- | :-- |
| Stejná síť | 192.168.1.110 | 192.168.1.9 | přímo |
| Vzdálená síť | 192.168.1.110 | 172.16.1.99 | přes [[default gateway]] |

**Souvisí:** [[IPv4]], [[IPv6]], [[maska podsítě]], [[délka prefixu]], [[MAC adresa]], [[NAT]], [[DHCP]], [[default gateway]]
