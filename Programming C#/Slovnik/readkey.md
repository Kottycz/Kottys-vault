---
aliases: [ReadKey, Console.ReadKey]
tags: [slovnik]
---

# ReadKey

**Metoda, která počká na stisk libovolné klávesy a vrátí ji – pro načtení jednoho znaku bez Enteru.**

```csharp
Console.ReadKey();
```

---

## Podrobně

### Rozdíl oproti ReadLine

| | [[readline\|ReadLine]] | ReadKey |
| :-- | :-- | :-- |
| Čeká na | **Enter** | **jednu klávesu** |
| Načte | celý řádek ([[string]]) | jednu klávesu |
| Použití | zadání textu a čísel | „stiskni klávesu", ovládání |

### Počkání před zavřením okna

Když spustíš program mimo Visual Studio, okno se po doběhnutí hned zavře. `ReadKey()` na konci ho podrží otevřené:

```csharp
Console.WriteLine("Hotovo.");
Console.ReadKey();   // počká na stisk klávesy
```

### Zjištění, která klávesa byla stisknuta

Metoda vrací objekt s informací o klávese:

```csharp
ConsoleKeyInfo k = Console.ReadKey();
if (k.Key == ConsoleKey.Escape)
{
    Console.WriteLine("Konec");
}
Console.WriteLine(k.KeyChar);   // znak, který se stiskl
```

### Skrytí znaku

`Console.ReadKey(true)` načte klávesu, ale **nevypíše** ji do [[konzole]] – hodí se pro menu a hry.

### Příklad – menu

```csharp
Console.WriteLine("1 – start, 2 – konec");
char volba = Console.ReadKey(true).KeyChar;
switch (volba)
{
    case '1': /* … */ break;
    case '2': /* … */ break;
}
```

Vrácený znak je [[char]] – porovnává se v jednoduchých uvozovkách. Hodí se spolu se [[switch|switchem]].

**Souvisí:** [[readline]], [[konzole]], [[char]], [[switch]]
