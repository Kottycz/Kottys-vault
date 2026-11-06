---
aliases: [int, Int32]
tags: [slovnik]
---

# int

**Celé číslo** (bez desetinné čárky), 32 bitů. Nejpoužívanější číselný [[datovy_typ|datový typ]].

```csharp
int vek = 17;
```

---

## Podrobně

### Rozsah

| | Hodnota |
| :-- | :-- |
| Velikost | 32 bitů (4 bajty) |
| Minimum | −2 147 483 648 |
| Maximum | 2 147 483 647 |
| Výchozí hodnota | 0 |

Plný název typu je `System.Int32`, `int` je jen zkratka.

### Dělení intů

Dělení dvou intů dá zase int – desetinná část se **zahodí** (ne zaokrouhlí). Viz [[celociselne_deleni|celočíselné dělení]].

```csharp
int x = 7 / 2;   // 3
int z = 7 % 2;   // 1 (zbytek po dělení)
```

### Přetečení

Když výsledek překročí maximum, "přeteče" a začne od minima – program nespadne, jen dá nesmysl.

```csharp
int max = int.MaxValue;   // 2147483647
max = max + 1;            // -2147483648
```

Na větší čísla existuje `long` (64 bitů, cca ±9,2 · 10¹⁸).

### Převod z textu

Vstup z [[readline|ReadLine]] je [[string]], na int se převede přes [[parse|int.Parse]]:

```csharp
int a = int.Parse(Console.ReadLine());
```

### Další celočíselné typy

| Typ | Velikost | Rozsah |
| :-- | :-- | :-- |
| `byte` | 8 bitů | 0 až 255 |
| `short` | 16 bitů | −32 768 až 32 767 |
| `int` | 32 bitů | cca ±2,1 miliardy |
| `long` | 64 bitů | cca ±9,2 · 10¹⁸ |

**Souvisí:** [[datovy_typ]], [[double]], [[float]], [[celociselne_deleni]], [[pretypovani]], [[parse]]
