# Navigace v IOSu

## Režimy

- **Uživatelský režim EXEC** – omezené možnosti, užitečný pro základní operace.
- **Privilegovaný režim EXEC** – pro spuštění konfiguračních příkazů musí správce přistupovat k tomuto režimu.
- **Režim konfigurace linky** – konfigurace přístupu přes konzoli, [[SSH]], [[Telnet]] nebo AUX.
- **Režim konfigurace rozhraní** – konfigurace portu [[switch|přepínače]] nebo síťového rozhraní [[router|routeru]].

Viz [[IOS]].

## Základní příkazy pro přechod mezi režimy (Cisco IOS)

| Příkaz | Význam |
| :-- | :-- |
| `enable` | Vstup do privilegovaného režimu EXEC |
| `disable` | Návrat do uživatelského režimu EXEC |
| `configure terminal` | Vstup do globální konfigurace |
| `exit` | Návrat o jeden režim zpět |
| `end` | Návrat přímo do privilegovaného režimu EXEC |
