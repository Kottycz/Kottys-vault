---
aliases: [double, Double]
tags: [slovnik]
---

# double

**Desetinné číslo s dvojitou přesností** (64 bitů, cca 15–16 platných číslic). Výchozí typ pro desetinná čísla.

```csharp
double c = 5.6;
```

---

## Podrobně

### Rozsah a přesnost

| | Hodnota |
| :-- | :-- |
| Velikost | 64 bitů (8 bajtů) |
| Přesnost | cca 15–16 platných číslic |
| Rozsah | cca ±1,7 · 10³⁰⁸ |
| Výchozí hodnota | 0 |

### Výchozí desetinný typ

Každé desetinné číslo zapsané v kódu (`5.6`, `1.0`) je automaticky double – na rozdíl od [[float]] se nepíše žádné písmeno. Všechny funkce z [[math|Math]] vrací double.

### Pozor na celá čísla

Do doublu jde uložit výsledek dělení intů, ale to dělení proběhne **ještě jako int**:

```csharp
double d = 3 / 4;     // 0 – dělí se dva inty
double d = 3.0 / 4;   // 0.75
```

Viz [[celociselne_deleni|celočíselné dělení]].

### Speciální hodnoty

Double umí i "nečísla", která vzniknou u neplatných operací – program nespadne:

- `NaN` (Not a Number) – např. `Math.Sqrt(-1)`
- `Infinity` – např. `1.0 / 0`

### double vs. float vs. decimal

| Typ | Přesnost | Použití |
| :-- | :-- | :-- |
| [[float]] | ~7 číslic | hry, grafika |
| `double` | ~15 číslic | běžné výpočty |
| `decimal` | ~28 číslic | peníze (počítá v desítkové soustavě, bez chyb zaokrouhlení) |

**Souvisí:** [[datovy_typ]], [[float]], [[int]], [[math]], [[celociselne_deleni]], [[pretypovani]]
