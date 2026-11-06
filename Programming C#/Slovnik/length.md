---
aliases: [Length, délka pole, GetLength]
tags: [slovnik]
---

# Length

**Vlastnost pole, která vrací jeho délku – celkový počet prvků.**

```csharp
int[] a = new int[5];
Console.WriteLine(a.Length);   // 5
```

---

## Podrobně

### Použití

Nejčastěji v podmínce [[for|cyklu for]], aby se nemuselo počítat s pevným číslem:

```csharp
for (int i = 0; i < a.Length; i++)
{
    Console.WriteLine(a[i]);
}
```

Když pak pole zvětšíš nebo zmenšíš v deklaraci, cyklus funguje dál beze změny.

### Vztah k indexu

Pole o délce `n` má [[index|indexy]] `0` až `n − 1`. Proto je podmínka cyklu `i < a.Length`, **ne** `<=`.

### Length je vlastnost, ne metoda

Píše se **bez závorek**: `a.Length`, ne `a.Length()`.

### U dvourozměrného pole

[[dvourozmerne_pole|Dvourozměrné pole]] má `Length` = **celkový počet prvků** (řádky × sloupce). Počty v jednotlivých rozměrech vrací metoda **GetLength()**:

```csharp
int[,] m = new int[3, 4];
m.Length;          // 12  (3 × 4)
m.GetLength(0);    // 3   (řádky)
m.GetLength(1);    // 4   (sloupce)
```

Parametr `0` = první rozměr (řádky), `1` = druhý (sloupce).

### Length u řetězce

[[string]] má také `Length` – počet znaků:

```csharp
"Kotty".Length   // 5
```

### Length vs. Count

| | Length | Count |
| :-- | :-- | :-- |
| Používá se u | [[pole]], [[string]] | seznam (`List<T>`) – viz [[kolekce]] |

**Souvisí:** [[pole]], [[index]], [[for]], [[dvourozmerne_pole]], [[string]]
