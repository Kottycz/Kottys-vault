---
aliases: [banner, MOTD, message of the day]
tags: [slovnik]
---

# banner MOTD

**Banner MOTD** (Message Of The Day) – **text, který se zobrazí při přihlášení** k zařízení; používá se jako **právní upozornění** na neoprávněný přístup. Příklad: „Authorized Access Only!“.

---

## Podrobně

### Konfigurace

```
R1(config)# banner motd #Authorized Access Only!#
```

- `#` je **oddělovač** – libovolný znak, který se v textu nevyskytuje; začátek i konec bannerem ohraničí stejný znak.
- Text může mít víc řádků:

```
Router(config)# banner motd #
Vstup povolen pouze autorizovaným osobám!
Jakýkoli neoprávněný přístup bude zaznamenán.
#
```

### Proč

- Právní ochrana (kdo se přihlásí, byl varován).
- **Nepsát** do bannerů „Vítejte“ ani informace o zařízení (verze, jméno firmy) – usnadňuje útok.

### Oddělovač

Text banneru se uzavře **oddělovacím znakem**, který se v textu nesmí objevit (často `#`, `$` nebo `%`):

```
R1(config)# banner motd #Pristup jen pro opravnene osoby!#
```

Jakmile IOS narazí podruhé na `#`, banner skončí. Text může být i na víc řádků.

### Co do banneru nepsat

- slova jako „Vítejte" nebo „Welcome" – u soudu by šlo tvrdit, že útočník byl pozván,
- název firmy, model zařízení, verzi IOS, IP adresy – útočníkovi to usnadní práci.

Správně: jen varování, že přístup je povolen pouze oprávněným osobám a je monitorovaný.

### Další bannery

| Banner | Kdy se zobrazí |
| :-- | :-- |
| `banner motd` | jako první, ještě před přihlášením |
| `banner login` | po MOTD, před výzvou k zadání jména a hesla |
| `banner exec` | až po úspěšném přihlášení |

Ověření: `show running-config | include banner`.

**Souvisí:** [[IOS]], [[running-config]], [[SSH]], [[Telnet]]
