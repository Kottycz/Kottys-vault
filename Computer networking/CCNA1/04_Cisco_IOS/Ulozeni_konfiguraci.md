# Uložení konfigurací

## Konfigurační soubory

Existují dva systémové soubory, které ukládají konfiguraci zařízení:

- **[[startup-config]]** – uložený konfigurační soubor v paměti NVRAM. Obsahuje všechny příkazy, které zařízení použije při spuštění nebo restartu. Obsah se neztratí při vypnutí zařízení.
- **[[running-config]]** – konfigurace uložená v paměti RAM. Odráží aktuální konfiguraci; úprava okamžitě ovlivní provoz zařízení. RAM je volatilní paměť – při vypnutí nebo restartu ztratí veškerý obsah.

Zobrazení běžící konfigurace (privilegovaný režim EXEC, viz [[IOS]]):
```
show running-config
```

Při výpadku napájení nebo restartu se všechny neuložené změny ztratí. Uložení změn z running-config do startup-config:
```
copy running-config startup-config
```

## Změna spuštěné konfigurace

- Změněné příkazy odstranit jednotlivě, nebo zařízení znovu načíst příkazem `reload` (privilegovaný režim EXEC) – tím se obnoví startup-config.
- Pokud byly do spouštěcí konfigurace uloženy nežádoucí změny, může být nutné vymazat všechny konfigurace: smazat startup-config a restartovat zařízení.

```
erase startup-config
```
