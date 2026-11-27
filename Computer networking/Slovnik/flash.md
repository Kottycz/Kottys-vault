---
aliases: [flash paměť, flash:]
tags: [slovnik]
---

# flash

**Flash** – trvalá paměť zařízení Cisco, ve které je uložený samotný [[IOS]]. Přežije restart i vypnutí. Příklad: soubor `c2960-lanbasek9-mz.150-2.SE8.bin` ve flash.

---

## Podrobně

### Paměti zařízení Cisco

| Paměť | Obsah | Přežije restart |
| :-- | :-- | :-- |
| **Flash** | IOS | ano |
| RAM | [[running-config]] | ne |
| NVRAM | [[startup-config]] | ano |
| ROM | [[boot loader]], bootovací instrukce | ano |

### Příkazy

```
S1# show flash
S1# dir flash:
```

V [[boot loader|boot loaderu]]: `flash_init` (inicializace) a pak `dir flash:`.

### K čemu

- uložení a **výměna IOS** (nový obraz, záloha),
- boot proměnná `BOOT=flash:...` ukazuje, který soubor se načte.

### Práce se soubory ve flash

| Příkaz | Co dělá |
| :-- | :-- |
| `show flash:` / `dir flash:` | obsah flash a volné místo |
| `show version` | který IOS běží a odkud se načetl |
| `copy tftp: flash:` | nahraje nový IOS z [[TFTP]] serveru |
| `copy flash: tftp:` | záloha IOS na TFTP server |
| `delete flash:soubor` | smaže soubor |

### Aktualizace IOS

1. zkontrolovat, že se nový IOS do flash vejde (`show flash:`),
2. zálohovat starý IOS a konfiguraci,
3. nahrát nový soubor přes TFTP,
4. nastavit `boot system flash:novy-ios.bin`,
5. uložit konfiguraci a restartovat (`reload`).

### Co ještě ve flash bývá

Na switchi soubor `vlan.dat` s databází VLAN a `config.text`, což je [[startup-config]] (na switchi se ukládá do flash, na routeru do NVRAM).

**Souvisí:** [[IOS]], [[boot loader]], [[POST]], [[running-config]], [[startup-config]]
