---
aliases: [Konzole, Console]
tags: [slovnik]
---

# konzole

**Textové okno**, kam program vypisuje výstup a odkud čte vstup od uživatele. V C# přes třídu `Console`.

```csharp
Console.WriteLine("Hello, World!");
```

---

## Podrobně

### Konzolová aplikace

Nejjednodušší typ programu – nemá žádná okna ani tlačítka, jen text. Ve Visual Studiu se zakládá jako **Console App**. Hodí se na učení, protože se člověk soustředí jen na logiku.

### Hlavní metody třídy Console

| Metoda | Co dělá | Detail |
| :-- | :-- | :-- |
| `Console.WriteLine()` | vypíše text a odřádkuje | [[writeline]] |
| `Console.Write()` | vypíše text bez odřádkování | [[write]] |
| `Console.ReadLine()` | načte řádek od uživatele | [[readline]] |
| `Console.ReadKey()` | počká na stisk jedné klávesy | – |
| `Console.Clear()` | vymaže obrazovku | – |

### Výpis proměnných

Tři způsoby, jak dostat hodnotu proměnné do textu – viz [[vypis_promennych|výpis proměnných]].

### Tip – okno se hned zavře

Když program spustíš mimo Visual Studio, okno se po doběhnutí hned zavře. Na konec se dá dát:

```csharp
Console.ReadKey();   // počká na stisk klávesy
```

### Barvy

```csharp
Console.ForegroundColor = ConsoleColor.Green;
Console.WriteLine("zelený text");
Console.ResetColor();
```

**Souvisí:** [[writeline]], [[write]], [[readline]], [[vypis_promennych]], [[escape_sekvence]]
