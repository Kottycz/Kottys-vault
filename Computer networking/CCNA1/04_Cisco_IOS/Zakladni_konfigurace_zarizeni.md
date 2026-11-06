# Základní konfigurace zařízení

## Názvy zařízení

Pokyny pro pojmenování hostitelů:
- začínat písmenem,
- neobsahovat mezery,
- končit písmenem nebo číslicí,
- používat pouze písmena, číslice a pomlčky,
- být kratší než 64 znaků.

## Pokyny pro hesla

- Používat hesla delší než osm znaků.
- Kombinovat velká a malá písmena, číslice, speciální znaky a/nebo číselné posloupnosti.
- Nepoužívat stejné heslo pro všechna zařízení.
- Nepoužívat běžná slova – dají se snadno uhodnout.

## Zabezpečení konzole

Zabezpečení privilegovaného přístupu EXEC (viz [[IOS]]):
```
enable secret PASSWORD
```

**Virtuální terminálové linky (VTY)** umožňují vzdálený přístup přes [[Telnet]] nebo [[SSH]]. Mnoho přepínačů Cisco podporuje až 16 linek VTY, číslovaných 0–15.

Zabezpečení linek VTY:
```
line vty 0 15
password PASSWORD
login
```

## Šifrování hesel

Soubory [[startup-config]] a [[running-config]] zobrazují většinu hesel v prostém textu – bezpečnostní hrozba, kdokoli s přístupem k souborům je uvidí.

Zašifrování všech hesel v prostém textu:
```
service password-encryption
```

Ověření příkazem `show running-config`.

## Zprávy v bannerech

Banner MOTD se konfiguruje příkazem `banner motd` (viz Základní konfigurace [[router|routeru]]).
