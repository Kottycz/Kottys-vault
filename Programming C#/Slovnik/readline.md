---
aliases: [ReadLine, Console.ReadLine]
tags: [slovnik]
---

# ReadLine

**Načte řádek textu od uživatele** (čeká, než napíše a zmáčkne Enter). Vrací vždy [[string]].

```csharp
string jmeno = Console.ReadLine();
```

---

## Podrobně

### Jak funguje

1. Program se na tomhle řádku **zastaví** a čeká.
2. Uživatel píše do [[konzole]].
3. Po stisku **Enter** se napsaný text (bez Enteru) vrátí jako string.

### Vždy string

I když uživatel napíše `42`, ReadLine vrátí text `"42"`, ne číslo. S textem nejde počítat – `"42" + 1` je `"421"`. Na číslo se musí převést přes [[parse|Parse]]:

```csharp
string e = Console.ReadLine();
int a = int.Parse(e);

// nebo rovnou na jednom řádku
int a = int.Parse(Console.ReadLine());
double c = double.Parse(Console.ReadLine());
```

### Výzva pro uživatele

ReadLine sám nic nevypíše – uživatel by nevěděl, co má zadat. Vždycky před něj dej výpis:

```csharp
Console.Write("Zadej stranu a: ");
int a = int.Parse(Console.ReadLine());
```

### Žluté varování (null)

Visual Studio u ReadLine ukazuje varování o možném `null`. ReadLine totiž vrátí `null`, když vstup skončí (třeba Ctrl+Z). V běžné konzolové aplikaci se to nestane, takže se to dá ignorovat.

### Chybný vstup

Když uživatel místo čísla napíše text, `int.Parse` **spadne**. Bezpečnější varianta je `int.TryParse` – viz [[parse]].

**Souvisí:** [[konzole]], [[parse]], [[string]], [[writeline]], [[write]]
