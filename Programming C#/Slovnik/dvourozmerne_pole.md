---
aliases: [Dvourozměrné pole, matice, 2D pole, GetLength]
tags: [slovnik]
---

# dvourozměrné pole

**[[pole|Pole]] se dvěma rozměry – tabulka s řádky a sloupci; k prvku se přistupuje dvěma indexy.**

```csharp
int[,] m = new int[3, 4];   // 3 řádky × 4 sloupce
m[1, 2] = 7;                // řádek 1, sloupec 2
```

---

## Podrobně

### Deklarace

```csharp
datovýTyp[,] názevPole = new datovýTyp[počet1, počet2];
```

Čárka v hranatých závorkách říká, že jde o **dva rozměry**. Počet1 = řádky, počet2 = sloupce.

### Rozměry – Length a GetLength

| Zápis | Vrací | Pro `new int[3, 4]` |
| :-- | :-- | :-- |
| `m.Length` | **celkový počet** prvků | `12` |
| `m.GetLength(0)` | počet **řádků** | `3` |
| `m.GetLength(1)` | počet **sloupců** | `4` |

Pozor: [[length|Length]] u dvourozměrného pole **nevrací počet řádků**, ale všech prvků dohromady.

### Procházení – vnořené cykly

Na tabulku jsou potřeba **dva [[for|cykly]]** – vnější pro řádky, vnitřní pro sloupce:

```csharp
for (int r = 0; r < m.GetLength(0); r++)
{
    for (int s = 0; s < m.GetLength(1); s++)
    {
        Console.Write(m[r, s] + " ");
    }
    Console.WriteLine();
}
```

Takhle se matice vypíše jako tabulka.

### Naplnění hodnotami

```csharp
int[,] m = { { 1, 2, 3 },
             { 4, 5, 6 } };    // 2 řádky × 3 sloupce
```

### foreach

[[foreach]] projde dvourozměrné pole **všechny prvky za sebou** (po řádcích), ale nevíš, ve kterém řádku jsi.

### Příklady použití

- matice v matematice
- hrací plocha (piškvorky, šachy, lodě)
- tabulka známek (žáci × předměty)

**Souvisí:** [[pole]], [[length]], [[index]], [[for]], [[cyklus]], [[foreach]]
