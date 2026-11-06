---
aliases: [Write, Console.Write]
tags: [slovnik]
---

# Write

**Vypíše text do [[konzole]] bez odřádkování** – další výpis pokračuje na stejném řádku.

```csharp
Console.Write("roman");
Console.WriteLine(" best");   // roman best
```

---

## Podrobně

### Rozdíl oproti WriteLine

| | `Write` | [[writeline|WriteLine]] |
| :-- | :-- | :-- |
| Po výpisu | kurzor zůstane na řádku | kurzor skočí na nový řádek |
| Bez parametru | nejde | vypíše prázdný řádek |

### Typické použití – výzva ke vstupu

Když chceš, aby uživatel psal hned za otázku, ne na další řádek:

```csharp
Console.Write("Zadej číslo: ");
int a = int.Parse(Console.ReadLine());
```

Výstup:

```
Zadej číslo: 5
```

S `WriteLine` by se číslo psalo až pod otázku.

### Ruční odřádkování

Nový řádek jde vložit i do Write přes [[escape_sekvence|escape sekvenci]] `\n`:

```csharp
Console.Write("roman\n\n");   // vypíše "roman" a 2× odřádkuje
```

`Console.Write("text\n")` tak dělá totéž co `Console.WriteLine("text")`.

### Výpis víc věcí na jeden řádek

```csharp
Console.Write("a = ");
Console.Write(a);
Console.Write(", b = ");
Console.WriteLine(b);
// a = 5, b = 3
```

Jednodušší je ale jeden WriteLine s [[vypis_promennych|interpolací]].

**Souvisí:** [[konzole]], [[writeline]], [[escape_sekvence]], [[readline]]
