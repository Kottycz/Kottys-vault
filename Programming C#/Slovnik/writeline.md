---
aliases: [WriteLine, Console.WriteLine]
tags: [slovnik]
---

# WriteLine

**Vypíše text do [[konzole]] a odřádkuje** – další výpis začne na novém řádku.

```csharp
Console.WriteLine("Hello, World!");
```

---

## Podrobně

### Co jde vypsat

Cokoliv – text, číslo, proměnnou, výsledek výpočtu. Nečíselné i číselné hodnoty se automaticky převedou na text.

```csharp
Console.WriteLine("text");
Console.WriteLine(42);
Console.WriteLine(a);
Console.WriteLine(a + b);
```

### Prázdný řádek

Bez parametru vypíše jen odřádkování – hodí se na oddělení bloků výstupu:

```csharp
Console.WriteLine();
```

### WriteLine vs. Write

```csharp
Console.Write("roman");
Console.WriteLine(" best");
Console.WriteLine("dalsi");
```

Výstup:

```
roman best
dalsi
```

[[write|Write]] nechá kurzor na stejném řádku, WriteLine ho posune na další.

### Výpis s proměnnými

```csharp
Console.WriteLine("a = " + a);        // spojení
Console.WriteLine("a = {0}", a);      // formát
Console.WriteLine($"a = {a}");        // interpolace
```

Podrobně v [[vypis_promennych|výpisu proměnných]].

### Pozor na spojování čísel

```csharp
Console.WriteLine("součet: " + 2 + 3);     // součet: 23
Console.WriteLine("součet: " + (2 + 3));   // součet: 5
```

Jakmile je vlevo text, `+` už čísla nesčítá, ale lepí jako text. Pomůžou závorky nebo interpolace.

**Souvisí:** [[konzole]], [[write]], [[readline]], [[vypis_promennych]], [[escape_sekvence]]
