---
aliases: [float, Single]
tags: [slovnik]
---

# float

**Desetinné číslo s jednoduchou přesností** (32 bitů, cca 7 platných číslic). Za číslo se píše `f`.

```csharp
float b = 6.4f;
```

---

## Podrobně

### Rozsah a přesnost

| | Hodnota |
| :-- | :-- |
| Velikost | 32 bitů (4 bajty) |
| Přesnost | cca 6–7 platných číslic |
| Rozsah | cca ±3,4 · 10³⁸ |
| Výchozí hodnota | 0 |

### Proč to `f`

Každé desetinné číslo v kódu (`6.4`) je v C# automaticky [[double]]. Double se do floatu sám nepřevede (ztratila by se přesnost), takže bez `f` kompilátor hlásí chybu:

```csharp
float b = 6.4;    // CHYBA
float b = 6.4f;   // OK
```

### Nepřesnost

Desetinná čísla se v počítači ukládají ve dvojkové soustavě a některá (např. 0.1) nejdou uložit přesně. U floatu je chyba vidět dřív než u doublu:

```csharp
float x = 0.1f + 0.2f;   // 0.3 (zaokrouhleně), ale ne přesně
```

Proto se desetinná čísla **neporovnávají přes `==`**, ale kontroluje se, jestli je rozdíl dost malý.

### Kdy použít

Hlavně tam, kde záleží na paměti a rychlosti – hry (Unity používá float), grafika. Pro běžné výpočty je lepší [[double]].

### Převod z doublu

Výsledky z [[math|Math]] jsou double, na float se musí [[pretypovani|přetypovat]]:

```csharp
float b = (float)Math.Sqrt(2);
```

**Souvisí:** [[datovy_typ]], [[double]], [[int]], [[pretypovani]], [[math]]
