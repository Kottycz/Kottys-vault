---
aliases: [startovací konfigurace, startup config]
tags: [slovnik]
---

# startup-config

**Uložená konfigurace v paměti NVRAM**, kterou zařízení načte při startu. Přežije restart i výpadek napájení.

---

## Podrobně

### Jak to funguje při startu

```
1. Zapnutí zařízení
2. Načte se IOS (operační systém)
3. Ze NVRAM se načte startup-config
4. Zkopíruje se do RAM jako [[running-config]]
5. Zařízení jede podle ní
```

Když startup-config neexistuje (nové nebo vymazané zařízení), spustí se **setup dialog** (průvodce základní konfigurací).

### Vztah k running-config

```
NVRAM                        RAM
startup-config  ──start──►   [[running-config]]
                ◄──copy──
                (ruční uložení)
```

Změny se dějí v running-config; do startup-config se dostanou **jen když je uložíš**:

```
Switch# copy running-config startup-config
```

### Užitečné příkazy

| Příkaz | Co dělá |
| :-- | :-- |
| `show startup-config` | zobrazí uloženou konfiguraci |
| `copy running-config startup-config` | uloží aktuální stav |
| `erase startup-config` | smaže uloženou konfiguraci |
| `reload` | restartuje zařízení |

### Zálohování na server

Konfiguraci je dobré zálohovat i mimo zařízení, např. na TFTP server:

```
Switch# copy running-config tftp:
```

### Typy pamětí na Cisco zařízení

| Paměť | Obsah | Přežije restart |
| :-- | :-- | :-- |
| **RAM** | running-config, tabulky ([[ARP]], MAC) | ne |
| **NVRAM** | startup-config | ano |
| **Flash** | IOS (operační systém) | ano |
| **ROM** | bootovací instrukce | ano |

**Souvisí:** [[running-config]], [[SVI]], [[switch]], [[router]]
