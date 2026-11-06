---
aliases: [Operand, operandy, unární operátor, binární operátor, prefix, postfix]
tags: [slovnik]
---

# operand

**Hodnota nebo proměnná, se kterou [[operator|operátor]] pracuje. Podle počtu operandů se operátory dělí na unární, binární a ternární.**

```csharp
int c = a + b;   // + je operátor, a a b jsou operandy
```

---

## Podrobně

### Dělení podle počtu operandů

| Typ | Operandy | Příklad |
| :-- | :-- | :-- |
| **unární** | jeden | `++i`, `i++`, `!a`, `-x` |
| **binární** | dva | `a + b`, `a > b`, `a && b` |
| **ternární** | tři | `x > 1 ? 1 : 0` |

### Unární operátory

Operují s **jedním** operandem. Nejznámější je [[inkrement]] a dekrement, které mají dvě podoby:

| Podoba | Zápis | Co se děje |
| :-- | :-- | :-- |
| **prefixová** | `++i` | **nejdřív se změní** hodnota proměnné, pak se vyhodnotí |
| **postfixová** | `i++` | **nejdřív se vyhodnotí** proměnná, pak se změní její hodnota |

```csharp
int i = 5;
int a = i++;   // a = 5, i = 6
int b = ++i;   // b = 7, i = 7
```

Další unární: `!` (negace – viz [[logicke_operatory]]), `-` (záporné znaménko).

### Binární operátory

Nejběžnější – dva operandy kolem symbolu: [[aritmeticke_operatory|aritmetické]], [[relacni_operatory|relační]], [[logicke_operatory|logické]] (`&&`, `||`), [[prirazeni|přiřazovací]].

Znaménko `+` je zároveň **sloučení řetězců**: `"ab" + "cd"` → `"abcd"`.

### Ternární operátor

Jediný se **třemi** operandy: podmínka, hodnota při `true`, hodnota při `false`. Viz [[ternarni_operator]].

**Souvisí:** [[operator]], [[inkrement]], [[ternarni_operator]], [[logicke_operatory]], [[aritmeticke_operatory]], [[relacni_operatory]]
