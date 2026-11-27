---
aliases: [terminal monitor, terminal no monitor]
tags: [slovnik]
---

# terminal monitor

**Příkaz Cisco [[IOS]], který zapne zobrazování systémových zpráv a výstupu [[debug]] i při vzdáleném připojení** (SSH, Telnet).

```
terminal monitor
```

---

## Podrobně

### Problém, který řeší

Některé zprávy systému IOS se automaticky zobrazují při připojení **ke konzoli**, ale **ne při vzdáleném připojení**. Ladicí výstup ([[debug]]) se tak ve výchozím nastavení objeví jen u konzole. Kdo je připojen na dálku, zprávy neuvidí.

### Jak se používá

```
Router# terminal monitor
Router# debug ip icmp
```

Po zadání se zprávy zobrazují i v aktuální vzdálené relaci.

### Platí jen pro aktuální relaci

Nastavení se po odhlášení ztratí – při příštím připojení se musí zadat znovu.

### Vypnutí

```
terminal no monitor
```

### Kdy ho použít

Připojíš se k routeru přes [[SSH]] a zapneš `debug ip icmp`. Bez `terminal monitor` neuvidíš nic, protože systémové zprávy jdou jen na konzoli. Po `terminal monitor` se ti zobrazují i ve tvém SSH okně.

### Související příkazy

| Příkaz | K čemu |
| :-- | :-- |
| `terminal monitor` | zapne zprávy pro aktuální VTY relaci |
| `terminal no monitor` | vypne je |
| `logging synchronous` (v line) | zprávy nepřeruší rozepsaný příkaz |
| `show logging` | zobrazí uložené systémové zprávy |

### Na konzoli není potřeba

Na konzoli (připojení kabelem) se zprávy zobrazují automaticky. `terminal monitor` je jen pro vzdálené připojení přes VTY.

**Souvisí:** [[debug]], [[IOS]], [[SSH]], [[Telnet]], [[Budovani_male_site]]
