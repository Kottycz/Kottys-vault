# Spuštění switche a obnova

Viz [[IOS|Cisco IOS]], rozcestník [[Basic_Device_Configuration]].

## Boot sekvence switche

1. **[[POST]]** – test hardwaru po zapnutí.
2. Spuštění **[[boot loader|boot loaderu]]** (malý program v ROM).
3. Inicializace **CPU** (registry).
4. Inicializace **[[flash]] filesystému**.
5. Načtení **[[IOS]]** a předání řízení.

Boot loader hledá IOS podle proměnné **BOOT**. Ručně: `boot system`, kontrola `show boot`.

## Obnova po pádu (boot loader)

Když IOS chybí nebo je poškozený, switch skončí v promptu `switch:`.

**Postup:**

- Odpojit napájení, **držet tlačítko Mode**, zapnout, pustit po rozsvícení LED.
- `help` nebo `?` – seznam příkazů.
- `set` – ukáže proměnnou BOOT.
- `flash_init` – inicializace flash, `dir flash:` – soubory.

```
switch: set
BOOT=flash:/c2960-lanbasek9-mz.122-55.SE7/c2960-lanbasek9-mz.122-55.SE7.bin
switch: flash_init
Initializing Flash...
...done Initializing Flash.
switch: dir flash:
```

**Nastavení nového IOS a start:**

```
switch: BOOT=flash:c2960-lanbasek9-mz.150-2.SE8.bin
switch: set
switch: boot
```

Boot loader umí: inicializace a formátování flash, instalace nového IOS, změna BOOT, **obnova ztraceného hesla**.

## LED indikátory switche

Catalyst 2960: LED 1–6 vlevo, tlačítko **Mode** (7) přepíná režim LED portů (8): stav, duplex, rychlost, PoE. Podrobně [[LED switche]].

| LED | Význam |
|---|---|
| **[[SYST]]** | napájení a funkce systému: vypnuto = bez napájení, zelená = OK, oranžová = napájení je, ale chyba |
| **[[RPS]]** | záložní zdroj: vypnuto = není/nepřipojen, zelená = připraven, blikající zelená = nedostupný (napájí jiné zařízení), oranžová = standby/chyba, blikající oranžová = vlastní zdroj switche selhal a napájí RPS |
| **STAT** | režim stavu portu (výchozí): zelená = režim zvolen |
| **DUPLX** | režim [[duplex]]: LED portu zelená = full-duplex, zhasnutá = half-duplex |
| **SPEED** | režim rychlost: zhasnutá = 10 Mb/s, zelená = 100 Mb/s, blikající zelená = 1000 Mb/s |
| **[[PoE]]** | režim PoE (jen když je podporováno) |

**Barvy LED portu v režimu STAT:**

- vypnuto = není link nebo port je administrativně vypnutý (shutdown)
- zelená = link je
- blikající zelená = aktivita (odesílá/přijímá)
- střídavě zelená–oranžová = chyba linku
- oranžová = port je blokován (ochrana proti smyčce, ~30 s po aktivaci je to normální)
- blikající oranžová = port blokován kvůli možné smyčce

**PoE LED v režimu PoE:**

- zelená = PoE zapnuto
- střídavě zelená–oranžová = PoE odepřeno (příkon by překročil kapacitu switche)
- blikající oranžová = PoE vypnuto kvůli chybě
- oranžová = PoE na portu zakázáno

Související: [[Navigace_v_IOSu]], [[Ulozeni_konfiguraci]]
