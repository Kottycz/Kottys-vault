---
aliases: [bootloader, boot loader software]
tags: [slovnik]
---

# boot loader

**Boot loader** – malý program v ROM, který se spustí po [[POST]] a **najde a načte [[IOS]]**. Když IOS chybí nebo je poškozený, switch skončí v promptu `switch:` a opravuje se právě tady.

---

## Podrobně

### Pořadí startu switche

1. [[POST]] – test hardwaru
2. **boot loader**
3. inicializace CPU
4. inicializace [[flash]] filesystému
5. načtení IOS

Boot loader hledá IOS podle proměnné **BOOT** (`show boot`, `boot system`).

### Přístup do boot loaderu

Odpojit napájení, **držet tlačítko Mode**, zapnout a po rozsvícení LED pustit. Objeví se `switch:`.

### Příkazy

| Příkaz | Co dělá |
| :-- | :-- |
| `help` / `?` | seznam příkazů |
| `set` | zobrazí proměnné, hlavně `BOOT` |
| `flash_init` | inicializace flash |
| `dir flash:` | soubory ve flash |
| `BOOT=flash:soubor.bin` | nastaví cestu k IOS |
| `boot` | spustí IOS podle BOOT |

```
switch: flash_init
switch: dir flash:
switch: BOOT=flash:c2960-lanbasek9-mz.150-2.SE8.bin
switch: set
switch: boot
```

### Další možnosti

Formátování flash, instalace nového IOS, změna BOOT, **obnova ztraceného hesla**.

### Proměnná BOOT

Kde hledat IOS určuje proměnná **BOOT**. Nastaví se příkazem:

```
S1(config)# boot system flash:/c2960-lanbasek9-mz.150-2.SE.bin
```

Když není nastavená, switch zkusí načíst první spustitelný soubor, který ve [[flash]] najde.

### Obnova hesla na switchi

1. vypnout switch, držet tlačítko **Mode** a zapnout → boot loader,
2. `flash_init`, pak přejmenovat konfiguraci (`rename flash:config.text flash:config.old`),
3. `boot` → switch naběhne bez konfigurace, bez hesla,
4. vrátit soubor, načíst ho do running-config, nastavit nové heslo a uložit.

### Router: ROMMON

Router má obdobu boot loaderu jménem **ROMMON** (prompt `rommon 1 >`). Obnova hesla:

```
rommon 1 > confreg 0x2142
rommon 2 > reset
```

Registr `0x2142` řekne routeru, ať při startu ignoruje [[startup-config]]. Po nastavení nového hesla se registr vrátí na `0x2102` (`config-register 0x2102`).

**Souvisí:** [[IOS]], [[POST]], [[flash]], [[switch]], [[running-config]], [[startup-config]]
