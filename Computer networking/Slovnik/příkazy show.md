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

**Souvisí:** [[IOS]], [[running-config]], [[ARP]], [[router]], [[ipconfig]], [[CDP]], [[Budovani_male_site]]
