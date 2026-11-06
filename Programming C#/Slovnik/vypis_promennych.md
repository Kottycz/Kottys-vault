---
aliases: [Výpis proměnných, Interpolace řetězců]
tags: [slovnik]
---

# výpis proměnných

**Tři způsoby, jak dostat hodnotu proměnné do textu**: spojení `+`, formát `{0}` a interpolace `$"{a}"`.

```csharp
Console.WriteLine($"hodnota a: {a}");
```

---

## Podrobně

### Tři způsoby

```csharp
int a = 5, b = 3;

Console.WriteLine("a: " + a + " b: " + b);          // 1. spojení
Console.WriteLine("a: {0} b: {1}", a, b);           // 2. formátování
Console.WriteLine($"a: {a} b: {b}");                // 3. interpolace
```

Všechny vypíšou `a: 5 b: 3`.

### 1. Spojení `+`

Nejjednodušší, ale u víc proměnných nepřehledné (hodně uvozovek a plusů). Pozor na čísla – `"x" + 2 + 3` je `"x23"`, ne `"x5"`.

### 2. Formátování `{0}`

Do textu se dají očíslované značky, hodnoty se doplní za čárkou ve stejném pořadí. `{0}` = první hodnota, `{1}` = druhá… Starší způsob, dnes se používá méně.

### 3. Interpolace `$`

Před uvozovky se dá `$` a proměnné se píšou **rovnou do složených závorek**. Nejčitelnější a nejpoužívanější. Do závorek jde dát i výpočet:

```csharp
Console.WriteLine($"součet: {a + b}");
Console.WriteLine($"obsah: {a * b} cm²");
```

### Formátování čísel

Za dvojtečku jde napsat, jak se má číslo zobrazit:

```csharp
double c = 3.14159;
Console.WriteLine($"{c:F2}");     // 3.14 (2 desetinná místa)
Console.WriteLine($"{c:F0}");     // 3
Console.WriteLine($"{1234567:N0}"); // 1 234 567
```

Hodí se hlavně u výsledků z [[math|Math]], které mají spoustu desetinných míst.

**Souvisí:** [[writeline]], [[write]], [[string]], [[konzole]]
