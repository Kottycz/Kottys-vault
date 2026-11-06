---
aliases: [Opakování 1, Operátory a proměnné]
tags: [opakovani, csharp]
---

# 01 – Operátory a deklarace proměnných

Opakování k testu.

## Operátory podle počtu [[operand|operandů]]

| Typ | Operandy | Příklad |
| :-- | :-- | :-- |
| **unární** | jeden | `++i`, `i++`, `!a` |
| **binární** | dva | `a + b` |
| **ternární** | tři | `x > 1 ? 1 : 0` |

**Unární [[inkrement|inkrementace]]** má dvě podoby:

- **prefixová** `++i` – nejdřív se změní hodnota, pak se vyhodnotí
- **postfixová** `i++` – nejdřív se vyhodnotí, pak se změní hodnota

## Rozdělení operátorů

| Skupina | Operátory |
| :-- | :-- |
| [[aritmeticke_operatory\|aritmetické]] | `+` `-` `*` `/` `%` |
| [[logicke_operatory\|logické]] | `!` `&&` `\|\|` |
| sloučení řetězců | `+` |
| [[inkrement\|inkrementace, dekrementace]] | `++` `--` |
| [[relacni_operatory\|relační]] (porovnávací) | `==` `!=` `>` `<` `>=` `<=` |
| [[prirazeni\|přiřazovací]] | `=` `+=` `-=` … |
| přístup k členům | `.` |
| indexování | `[]` |
| [[pretypovani\|přetypování]] | `()` |

## Deklarace proměnných

[[promenna|Proměnné]] se dělí podle toho, co je v nich uloženo:

- **[[hodnotovy_typ|hodnotové typy]]** – v proměnné je přímo hodnota
- **[[referencni_typ|odkazové (referenční) typy]]** – v proměnné je odkaz na data

### Hodnotové typy

| Skupina | Typy |
| :-- | :-- |
| celočíselné | [[int]], `long`, `short`, `byte` |
| s desetinnou čárkou | [[float]], [[double]] |
| speciální – větší přesnost, menší rozsah | [[decimal]] |
| logická hodnota | [[bool]] |
| znak | [[char]] |

U čísla typu [[float]] musí následovat písmeno `f`:

```csharp
float a = 5.65f;
```

### Referenční typy

- [[string]]
- `object` – viz [[object]]
- **pole** – viz [[05_Pole]]
- předávání referencí – [[ref]]

```csharp
static void Swap(ref int x, ref int y)
{
    int temp = x;
    x = y;
    y = temp;
}
```

Referenční typy mohou – na rozdíl od hodnotových – nabývat hodnoty **[[null|`null`]]**. Ta označuje, že reference neukazuje na žádná data.

**Souvisí:** [[02_Vstup_vystup]], [[03_Podminky]], [[04_Cykly]], [[05_Pole]]
