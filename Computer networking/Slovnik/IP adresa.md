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

### Jak zařízení pozná, jestli je cíl ve stejné síti

Provede **AND** své IP adresy s maskou a totéž s cílovou IP. Když vyjde stejná adresa sítě, cíl je lokální a pošle mu rámec přímo (zjistí jeho MAC přes [[ARP]]). Když ne, pošle rámec na [[default gateway|výchozí bránu]].

```
moje IP   192.168.1.10  AND 255.255.255.0 = 192.168.1.0
cíl       192.168.1.77  AND 255.255.255.0 = 192.168.1.0  → stejná síť
cíl       10.0.0.5      AND 255.255.255.0 = 10.0.0.0     → jiná síť, jde na bránu
```

### Typy adres podle komunikace

- [[unicast]] – jednomu zařízení,
- [[broadcast]] – všem v síti (jen IPv4),
- [[multicast]] – skupině,
- [[anycast]] – nejbližšímu ze skupiny (hlavně IPv6).

### Nastavení na Cisco

```
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# no shutdown
```

Ověření: `show ip interface brief`.

**Souvisí:** [[IPv4]], [[IPv6]], [[maska podsítě]], [[délka prefixu]], [[MAC adresa]], [[NAT]], [[DHCP]], [[default gateway]]
