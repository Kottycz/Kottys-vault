---
aliases: [late collisions, pozdní kolize]
tags: [slovnik]
---

# late collision

**Late collision** – [[kolize]], která nastane **až po odvysílání 512 bitů** rámce (64 B). V síti by se **nikdy neměla objevit**. Příklad: jeden konec linky je full, druhý half → half strana hlásí late collisions.

---

## Podrobně

### Příčiny

| Příčina | Popis |
| :-- | :-- |
| **[[duplex]] mismatch** | jedna strana [[full-duplex]], druhá [[half-duplex]]; late collisions vidíš na half straně |
| **Moc dlouhý kabel** | signál se k druhému konci dostane pozdě, nejčastější příčina u dlouhých tras |
| Vadný kabel / karta | méně časté |

### Řešení

- nastavit **stejný duplex** na obou koncích,
- zkrátit nebo vyměnit kabel,
- správně navržená a nakonfigurovaná síť late collisions nemá.

**Souvisí:** [[kolize]], [[duplex]], [[auto-negotiation]], [[CRC]], [[příkazy show]]
