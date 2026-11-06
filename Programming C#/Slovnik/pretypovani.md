---
aliases: [Přetypování, cast]
tags: [slovnik]
---

# přetypování

**Převod hodnoty na jiný [[datovy_typ|datový typ]]** – cílový typ se napíše do závorky před hodnotu.

```csharp
int a = (int)Math.Sqrt(2);   // 1.414… → 1
```

---

## Podrobně

### Implicitní vs. explicitní

| | Implicitní (automatické) | Explicitní (ruční) |
| :-- | :-- | :-- |
| Kdy | z menšího typu do většího | z většího do menšího |
| Ztráta dat | ne | může nastat |
| Zápis | nic se nepíše | `(typ)hodnota` |
| Příklad | `double d = 5;` | `int i = (int)5.7;` |

Kompilátor převod sám udělá jen tam, kde se nic neztratí. Kde by se mohla ztratit přesnost, musíš to napsat ručně – tím říkáš "vím, co dělám".

### Směr převodů

```
byte → short → int → long → float → double
         (implicitně doprava, explicitně doleva)
```

### Useknutí, ne zaokrouhlení

Při převodu desetinného čísla na [[int]] se desetinná část **zahodí**:

```csharp
(int)3.7    // 3
(int)-3.7   // -3
```

Když chceš zaokrouhlit, použij [[math|Math.Round]]:

```csharp
int a = (int)Math.Round(3.7);   // 4
```

### Přetypování kvůli dělení

Častý trik, jak se vyhnout [[celociselne_deleni|celočíselnému dělení]]:

```csharp
int a = 3, b = 4;
double d = (double)a / b;   // 0.75
double e = (double)(a / b); // 0 – přetypuje se až výsledek!
```

Záleží, **co** přetypuješ – přetypovat se musí operand, ne až výsledek.

### Přetypování vs. Parse

| | Přetypování | [[parse|Parse]] |
| :-- | :-- | :-- |
| Převádí | číslo → číslo | text → číslo |
| Příklad | `(int)3.7` | `int.Parse("3")` |

`(int)"5"` nefunguje – text se na číslo převádí jen přes Parse.

**Souvisí:** [[datovy_typ]], [[int]], [[double]], [[float]], [[celociselne_deleni]], [[parse]], [[math]]
