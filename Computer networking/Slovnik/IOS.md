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

**Souvisí:** [[running-config]], [[startup-config]], [[router]], [[switch]], [[SVI]], [[SSH]]
