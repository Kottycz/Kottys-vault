---
aliases: [vty, virtuální terminálové linky, line vty]
tags: [slovnik]
---

# VTY

**VTY** (Virtual Teletype) – **virtuální linky** pro **vzdálený přístup** k zařízení přes síť ([[SSH]] nebo [[Telnet]]). Každá vzdálená relace zabere jednu linku. Příklad: `line vty 0 15` = 16 souběžných vzdálených přihlášení na switch.

---

## Podrobně

- Switche Catalyst 2960: **0–15** (16 linek), routery obvykle **0–4**.
- Nejsou to fyzické porty, jen „sloty“ pro vzdálená spojení (na rozdíl od **console** linky, která je fyzický kabel).

### Konfigurace

```
S1(config)# line vty 0 15
S1(config-line)# transport input ssh
S1(config-line)# login local
S1(config-line)# exit
```

| Příkaz | Význam |
| :-- | :-- |
| `transport input ssh` | povolí **jen SSH**, [[Telnet]] se odmítne |
| `transport input all` | povolí vše (výchozí u starších IOS) |
| `login` | ověření heslem linky |
| `login local` | ověření proti lokální databázi (`username ... secret ...`) |

**Souvisí:** [[SSH]], [[Telnet]], [[IOS]], [[PuTTY]], [[running-config]]
