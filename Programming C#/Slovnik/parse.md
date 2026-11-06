---
aliases: [Parse, int.Parse, TryParse]
tags: [slovnik]
---

# Parse

**Převod textu na číslo** – `int.Parse()`, `double.Parse()`, `float.Parse()`. Používá se na vstup z [[readline|ReadLine]].

```csharp
int a = int.Parse(Console.ReadLine());
```

---

## Podrobně

### Proč je potřeba

[[readline|Console.ReadLine()]] vrací vždycky [[string]]. S textem `"5"` se nedá počítat, musí se nejdřív převést na číslo.

### Varianty

```csharp
int a = int.Parse("42");            // 42
double c = double.Parse("5.6");     // 5.6
float b = float.Parse("6.4");       // 6.4
bool f = bool.Parse("true");        // true
```

Pro každý [[datovy_typ|typ]] je vlastní `Parse` – typ před tečkou určuje, na co se převádí.

### Když vstup není číslo

Když uživatel napíše `ahoj` nebo `5.5` do `int.Parse`, program **spadne** s chybou `FormatException`.

### TryParse – bezpečná verze

`TryParse` nespadne – vrátí [[bool]], jestli se převod povedl, a číslo uloží přes `out`:

```csharp
if (int.TryParse(Console.ReadLine(), out int a))
{
    Console.WriteLine($"Zadal jsi {a}");
}
else
{
    Console.WriteLine("To není číslo");
}
```

Opakování, dokud uživatel nezadá platné číslo:

```csharp
int a;
while (!int.TryParse(Console.ReadLine(), out a))
{
    Console.Write("Neplatné číslo, zkus znovu: ");
}
```

### Desetinná čárka vs. tečka

`double.Parse` používá nastavení jazyka Windows. Na českém systému čeká **čárku** (`5,6`) – s tečkou (`5.6`) může spadnout nebo dát špatné číslo. Zadávej desetinná čísla tak, jak to čeká systém.

### Opačný směr – číslo na text

```csharp
string s = a.ToString();   // "42"
```

**Souvisí:** [[readline]], [[string]], [[int]], [[double]], [[datovy_typ]], [[pretypovani]]
