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

### Proč 512 bitů

Minimální rámec má 64 B = **512 bitů**. Za dobu, než se odvysílá 512 bitů, signál stihne doběhnout na konec sítě a zpátky (slot time). Kolize se proto při správně postavené síti musí objevit **během prvních 512 bitů**. Kolize později znamená, že síť je fyzicky moc velká nebo je chyba v nastavení.

### Rozdíl oproti běžné kolizi

| | Běžná kolize | Late collision |
| :-- | :-- | :-- |
| kdy | v prvních 64 B | po prvních 64 B |
| znovuodeslání | automaticky ([[CSMA-CD]]) | rámec se **neopakuje**, ztratí se |
| normální | na half-duplex ano | **nikdy** |

### Kde je hledat

```
S1# show interfaces fa0/1
  0 collisions, 25 late collision, 0 deferred
```

Late collisions na straně s half-duplex jsou typický znak [[duplex]] mismatch.

**Souvisí:** [[kolize]], [[duplex]], [[auto-negotiation]], [[CRC]], [[příkazy show]]
