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

### Kde je uložená

| Zařízení | Paměť | Soubor |
| :-- | :-- | :-- |
| router | NVRAM | startup-config |
| switch (Catalyst) | [[flash]] | `config.text` |

### Co se stane bez startup-config

Nové nebo vymazané zařízení nemá startup-config a po startu nabídne **Setup mode** („Would you like to enter the initial configuration dialog? [yes/no]"). Odpovíš `no` a konfiguruješ ručně.

### Postup při změnách

1. změnit konfiguraci (running-config),
2. ověřit, že vše funguje,
3. teprve pak uložit (`copy running-config startup-config` nebo `wr`).

Když se něco pokazí a ještě není uloženo, `reload` bez uložení vrátí zařízení do posledního uloženého stavu.

**Souvisí:** [[running-config]], [[SVI]], [[switch]], [[router]]
