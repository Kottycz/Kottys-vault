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

### Kolik linek

Většina Cisco zařízení má VTY linky **0 až 15** (16 současných vzdálených připojení), starší jen 0–4. Pro jistotu se konfigurují všechny:

```
R1(config)# line vty 0 15
R1(config-line)# transport input ssh
R1(config-line)# login local
R1(config-line)# exec-timeout 5 0
```

### Druhy linek

| Linka | Přístup |
| :-- | :-- |
| `line console 0` | kabelem přes konzolový port |
| `line vty 0 15` | po síti ([[SSH]], [[Telnet]]) |
| `line aux 0` | přes modem (starší routery) |

### Omezení odkud

`access-class` s ACL na VTY linkách pustí vzdálený přístup jen z vybraných adres (např. ze sítě adminů). Ověření připojených uživatelů: `show users`.

**Souvisí:** [[SSH]], [[Telnet]], [[IOS]], [[PuTTY]], [[running-config]]
