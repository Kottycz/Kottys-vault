---
aliases: [Relační operátory, porovnávací operátory, porovnání]
tags: [slovnik]
---

# relační operátory

**Operátory, které porovnávají dvě hodnoty a vrací [[bool]] – `true`, nebo `false`.**

```csharp
bool b = a > 5;   // true, když je a větší než 5
```

---

## Podrobně

### Přehled

| Operátor | Význam | Příklad (`a = 5`) | Výsledek |
| :-- | :-- | :-- | :-- |
| `==` | rovná se | `a == 5` | `true` |
| `!=` | nerovná se | `a != 5` | `false` |
| `>` | větší než | `a > 3` | `true` |
| `<` | menší než | `a < 3` | `false` |
| `>=` | větší nebo rovno | `a >= 5` | `true` |
| `<=` | menší nebo rovno | `a <= 4` | `false` |

### == není =

- `=` je [[prirazeni|přiřazení]] (uloží hodnotu)
- `==` je **porovnání** (zeptá se, jestli se rovnají)

### Kde se používají

V [[podminka|podmínkách]] a [[cyklus|cyklech]], kde je výsledek porovnání podmínkou pro provedení kódu:

```csharp
if (vek >= 18) { }
while (i < 10) { }
```

### Spojování porovnání

Víc porovnání se spojí [[logicke_operatory|logickými operátory]]:

```csharp
bool vRozsahu = a > 0 && a < 10;
```

V C# **nejde** psát `0 < a < 10` jako v matematice.

### Porovnání desetinných čísel

[[double]] a [[float]] nejsou přesné, takže `0.1 + 0.2 == 0.3` je **false**. Desetinná čísla se proto neporovnávají přes `==`, ale kontroluje se, jestli je rozdíl dost malý.

### Porovnání řetězců

`==` u [[string|řetězců]] porovnává **obsah** (ne adresu): `"ahoj" == "ahoj"` je `true`. Rozlišují se velká a malá písmena.

**Souvisí:** [[operator]], [[operand]], [[bool]], [[podminka]], [[logicke_operatory]], [[prirazeni]]
