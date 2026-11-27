---
aliases: [Internetwork Operating System, Cisco IOS]
tags: [slovnik]
---

# IOS

**Internetwork Operating System** – operační systém síťových zařízení Cisco ([[router|routerů]] a [[switch|switchů]]). Ovládá se přes příkazovou řádku (CLI).

---

## Podrobně

### Režimy

Příkazy fungují jen v odpovídajícím režimu – podle toho, co je za názvem zařízení:

| Výzva | Režim | K čemu |
| :-- | :-- | :-- |
| `Switch>` | **uživatelský** | základní příkazy, jen prohlížení |
| `Switch#` | **privilegovaný** (enable) | plná diagnostika, ukládání konfigurace |
| `Switch(config)#` | **globální konfigurační** | změny nastavení celého zařízení |
| `Switch(config-if)#` | **konfigurace rozhraní** | nastavení konkrétního portu |
| `Switch(config-line)#` | **konfigurace linky** | konzole, VTY (vzdálený přístup) |

### Pohyb mezi režimy

```
Switch>  enable                → Switch#
Switch#  configure terminal    → Switch(config)#
Switch(config)# interface g0/1 → Switch(config-if)#

exit    → o úroveň zpět
end     → rovnou do privilegovaného režimu (nebo Ctrl+Z)
```

### Užitečné zkratky

- **Tab** – doplní rozepsaný příkaz
- **?** – nápověda, co je možné napsat dál
- Příkazy lze **zkracovat**, dokud jsou jednoznačné: `conf t` = `configure terminal`, `sh run` = `show running-config`
- **Ctrl+C** – zruší příkaz, **Ctrl+Z** – ukončí konfiguraci

### Kde se IOS a konfigurace nacházejí

| Paměť | Obsah |
| :-- | :-- |
| **Flash** | samotný IOS (přežije restart) |
| **RAM** | [[running-config]] (nepřežije restart) |
| **NVRAM** | [[startup-config]] (přežije restart) |
| **ROM** | bootovací instrukce |

### Soubor IOS a jeho jméno

Jméno souboru prozradí platformu a verzi, např. `c2960-lanbasek9-mz.150-2.SE.bin`:

- `c2960` – pro switch Catalyst 2960,
- `lanbasek9` – sada funkcí, `k9` = podpora šifrování (nutné pro [[SSH]]),
- `150-2.SE` – verze 15.0(2)SE.

### Nápověda v IOS

| Co | Jak |
| :-- | :-- |
| seznam příkazů | `?` |
| dokončení příkazu | Tab |
| možnosti příkazu | `show ?` |
| historie | šipka nahoru, `show history` |
| zkrácené příkazy | `conf t`, `sh run`, `int g0/0` |

### Chybové hlášky

| Hláška | Význam |
| :-- | :-- |
| `% Ambiguous command` | zkratka sedí na víc příkazů, napiš víc písmen |
| `% Incomplete command` | chybí parametr |
| `% Invalid input detected at '^' marker` | chyba v místě, kam ukazuje `^` |

**Souvisí:** [[running-config]], [[startup-config]], [[router]], [[switch]], [[SVI]], [[SSH]]
