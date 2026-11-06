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

**Souvisí:** [[IOS]], [[running-config]], [[SSH]], [[Telnet]]
