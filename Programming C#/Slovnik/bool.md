---
aliases: [bool, boolean, Boolean]
tags: [slovnik]
---

# bool

**Logická hodnota** – může být jen `true` (pravda) nebo `false` (nepravda).

```csharp
bool jeVetsi = a > 5;
```

---

## Podrobně

### Vlastnosti

| | Hodnota |
| :-- | :-- |
| Hodnoty | `true`, `false` |
| Velikost | 1 bajt |
| Výchozí hodnota | `false` |

### Odkud se bere

Výsledek každého porovnání je bool:

| Operátor | Význam | Příklad |
| :-- | :-- | :-- |
| `==` | rovná se | `a == 5` |
| `!=` | nerovná se | `a != 5` |
| `>` / `<` | větší / menší | `a > 5` |
| `>=` / `<=` | větší nebo rovno / menší nebo rovno | `a >= 5` |

Pozor: `=` je [[prirazeni|přiřazení]], porovnání je `==`.

### Kombinování

Víc podmínek se spojuje [[logicke_operatory|logickými operátory]]:

```csharp
bool vRozsahu = a > 0 && a < 10;   // a zároveň
bool mimo = a < 0 || a > 10;       // nebo
bool opak = !vRozsahu;             // negace
```

### Použití

Bool řídí rozhodování v programu – podmínky `if`, cykly `while` a [[ternarni_operator|ternární operátor]]:

```csharp
if (jeVetsi)
{
    Console.WriteLine("a je větší než 5");
}
```

### Není to číslo

Na rozdíl od jazyka C nejde v C# použít `1` a `0` místo `true` a `false` – `if (1)` je chyba.

**Souvisí:** [[datovy_typ]], [[logicke_operatory]], [[ternarni_operator]], [[prirazeni]]
