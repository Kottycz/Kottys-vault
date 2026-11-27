---
aliases: [Link-Local Address, link-local adresa]
tags: [slovnik]
---

# LLA

**Link-Local Address** – [[IPv6]] adresa platná **jen v rámci jednoho segmentu sítě**. Nikdy se nesměruje dál. Prefix **fe80::/10**.

---

## Podrobně

### Klíčová vlastnost

Každé rozhraní s povoleným IPv6 má LLA **vždy** – vytvoří se automaticky při startu, i když není nastavená žádná jiná adresa a není v síti žádný [[router]] ani DHCP server.

### Jak vzniká

Prefix `fe80::` se spojí s ID rozhraní, které se získá jedním ze dvou způsobů:

- pomocí [[EUI-64]] z [[MAC adresa|MAC adresy]], nebo
- náhodně (dnes běžnější, kvůli soukromí)

Příklad výsledku: `fe80::204:61ff:fe9d:f156`

### K čemu slouží

| Použití | Popis |
| :-- | :-- |
| **[[NDP]]** | objevování sousedů, [[RS]]/[[RA]]/[[NS]] zprávy |
| **[[default gateway]]** | zařízení používá LLA routeru jako výchozí bránu |
| **Směrovací protokoly** | [[OSPF]]v3 a další si mezi routery povídají přes LLA |
| **Komunikace bez konfigurace** | dvě zařízení propojená kabelem spolu můžou hned mluvit |

### Zajímavost: brána je link-local

V IPv6 je výchozí brána skoro vždy **LLA routeru** (`fe80::1`), ne jeho globální adresa. Dává to smysl – brána je vždy na stejném segmentu a LLA se nemění, i když se změní prefix od poskytovatele.

### Identifikace rozhraní (zóna)

Protože stejná LLA může existovat na víc rozhraních, je potřeba určit, kterým rozhraním komunikovat:

```
ping fe80::1%eth0        (Linux)
ping fe80::1%12          (Windows, číslo rozhraní)
```

### Obdoba v IPv4

`169.254.x.x` – **APIPA**. Rozdíl je, že APIPA se použije jen když **selže [[DHCP]]** (je to nouzové řešení), zatímco LLA v IPv6 je normální a vždy přítomná.

### Ruční nastavení na routeru

```
R1(config-if)# ipv6 address fe80::1 link-local
```

Na všech rozhraních routeru může být stejná LLA `fe80::1`, protože platí jen v rámci jednoho segmentu. Klienti pak mají jako bránu jednoduchou adresu `fe80::1` místo dlouhé EUI-64.

### Ověření

```
R1# show ipv6 interface brief
GigabitEthernet0/0/0   [up/up]
    FE80::1
    2001:DB8:ACAD:1::1
```

První adresa je vždy LLA, pod ní [[GUA]].

### Ping na link-local

Na Windows se k LLA musí přidat číslo rozhraní (zóna): `ping fe80::1%12`. Systém jinak neví, na které síťové kartě má hledat, protože stejné fe80 adresy můžou existovat na víc kartách.

**Souvisí:** [[IPv6]], [[GUA]], [[ULA]], [[NDP]], [[EUI-64]], [[default gateway]], [[SLAAC]]
