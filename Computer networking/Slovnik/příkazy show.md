---
aliases: [show, show příkazy, show running-config, show ip route, show version]
tags: [slovnik]
---

# příkazy show

**Skupina příkazů Cisco [[IOS]], které jen zobrazují informace** o zařízení a jeho stavu. Nic nemění.

```
show ip interface brief
```

---

## Podrobně

### Příkazy z učiva

| Příkaz | Co ukáže |
| :-- | :-- |
| `show running-config` | aktuální konfiguraci uloženou v RAM ([[running-config]]) |
| `show interfaces` | stav a statistiky všech rozhraní (up/down, chyby, provoz) |
| `show ip interface` | podrobné IPv4 nastavení rozhraní |
| `show ip interface brief` | **zkrácený přehled** – rozhraní, IP adresa, stav |
| `show arp` | [[ARP]] tabulku – naučené dvojice IP ↔ MAC |
| `show ip route` | **směrovací tabulku** [[router\|routeru]] |
| `show protocols` | zapnuté síťové protokoly a stav rozhraní |
| `show version` | verzi IOS, model zařízení, dobu běhu, paměti |

### Kde se zadávají

Většina příkazů show se zadává v **privilegovaném režimu** (`Router#`). Nesmí se plést s konfigurací – show nic nenastavuje.

### Zkracování

Příkazy lze zkracovat, dokud jsou jednoznačné: `sh run` = `show running-config`, `sh ip int br` = `show ip interface brief`.

### Který použít jako první

- Nejrychlejší přehled o rozhraních: **`show ip interface brief`**
- Kontrola, co je aktuálně nakonfigurované: **`show running-config`**
- Jestli router umí cestu do cílové sítě: **`show ip route`**

### Srovnání s příkazy na hostiteli

Na počítači s Windows odpovídá `ipconfig /all` – viz [[ipconfig]].

### Filtrování výstupu

Dlouhý výstup se dá zúžit za svislou čárou:

| Filtr | Příklad | Co ukáže |
| :-- | :-- | :-- |
| `include` | `show running-config \| include hostname` | jen řádky s textem |
| `exclude` | `show ip interface brief \| exclude unassigned` | řádky bez textu |
| `begin` | `show running-config \| begin interface` | od prvního výskytu dál |
| `section` | `show running-config \| section ospf` | celou sekci konfigurace |

### Ovládání dlouhého výstupu

Při `--More--`: **mezerník** = další stránka, **Enter** = další řádek, jiná klávesa = konec. `terminal length 0` vypne stránkování úplně.

### Show v konfiguračním režimu

V `(config)#` režimu show nefunguje přímo, musí se před něj dát `do`: `R1(config)# do show ip interface brief`.

**Souvisí:** [[IOS]], [[running-config]], [[ARP]], [[router]], [[ipconfig]], [[CDP]], [[Budovani_male_site]]
