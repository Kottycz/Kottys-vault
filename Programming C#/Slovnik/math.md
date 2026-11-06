---
aliases: [Math, třída Math]
tags: [slovnik]
---

# Math

**Vestavěná třída s matematickými funkcemi** – mocniny, odmocniny, goniometrie, zaokrouhlování. Vrací [[double]].

```csharp
double c = Math.Sqrt(16);   // 4
```

---

## Podrobně

### Nejpoužívanější funkce

| Funkce | Co dělá | Příklad | Výsledek |
| :-- | :-- | :-- | :-- |
| `Math.Pow(x, n)` | x na n-tou | `Math.Pow(2, 3)` | 8 |
| `Math.Sqrt(x)` | druhá odmocnina | `Math.Sqrt(16)` | 4 |
| `Math.Abs(x)` | absolutní hodnota | `Math.Abs(-5)` | 5 |
| `Math.Round(x)` | zaokrouhlí | `Math.Round(2.6)` | 3 |
| `Math.Round(x, n)` | zaokrouhlí na n míst | `Math.Round(3.14159, 2)` | 3.14 |
| `Math.Floor(x)` | dolů | `Math.Floor(2.9)` | 2 |
| `Math.Ceiling(x)` | nahoru | `Math.Ceiling(2.1)` | 3 |
| `Math.Max(a, b)` | větší ze dvou | `Math.Max(3, 7)` | 7 |
| `Math.Min(a, b)` | menší ze dvou | `Math.Min(3, 7)` | 3 |
| `Math.Sin(x)` | sinus | `Math.Sin(0)` | 0 |

Konstanty: `Math.PI` (3,14159…), `Math.E` (2,71828…).

### Goniometrie je v radiánech

`Math.Sin`, `Math.Cos`, `Math.Tan` berou úhel v **radiánech**, ne ve stupních. Převod:

```csharp
double stupne = 30;
double rad = stupne * Math.PI / 180;
double s = Math.Sin(rad);   // 0.5
```

### Třetí (n-tá) odmocnina

Samostatná funkce na n-tou odmocninu není, dělá se přes mocninu 1/n:

```csharp
Math.Pow(1000, 1.0 / 3);   // 10
Math.Pow(1000, 1 / 3);     // 1 – CHYBA!
```

`1 / 3` je [[celociselne_deleni|celočíselné dělení]] = 0 a cokoliv na nultou je 1. Proto `1.0`.

### Výsledek je double

Když chceš výsledek uložit do intu nebo floatu, musíš [[pretypovani|přetypovat]]:

```csharp
int a = (int)Math.Sqrt(2);       // 1
float b = (float)Math.Sqrt(2);   // 1.4142135
```

### Použití v příkladech

```csharp
u = Math.Sqrt(a * a + b * b + c * c);   // úhlopříčka kvádru
obsah = Math.Sqrt(s * (s - a) * (s - b) * (s - c));   // Heronův vzorec
```

**Souvisí:** [[double]], [[pretypovani]], [[celociselne_deleni]], [[konstanta]], [[trida]]
