---
aliases: [Operátor, Operátory]
tags: [slovnik]
---

# operátor

**Symbol, který provádí operaci** s jednou nebo více hodnotami (operandy).

```csharp
int c = a + b;   // + je operátor, a a b jsou operandy
```

---

## Podrobně

### Druhy operátorů

| Druh | Operátory | Detail |
| :-- | :-- | :-- |
| Aritmetické | `+ - * / %` | [[aritmeticke_operatory]] |
| Přiřazovací | `= += -= *= /=` | [[prirazeni]] |
| Inkrement / dekrement | `++ --` | [[inkrement]] |
| Porovnávací | `== != > < >= <=` | výsledek je [[bool]] – viz [[relacni_operatory]] |
| Logické | `&& \|\| !` | [[logicke_operatory]] |
| Ternární | `? :` | [[ternarni_operator]] |

### Podle počtu operandů

- **Unární** – jeden operand: `a++`, `!b`, `-x`
- **Binární** – dva operandy: `a + b`, `a > b`
- **Ternární** – tři operandy: `a > 5 ? 1 : 2`

Podrobně viz [[operand]].

### Priorita

Stejně jako v matematice se nejdřív násobí, pak sčítá. Pořadí od nejvyšší priority (zjednodušeně):

1. `++ -- !` (unární)
2. `* / %`
3. `+ -`
4. `< > <= >=`
5. `== !=`
6. `&&`
7. `||`
8. `? :`
9. `= += -=…`

```csharp
int x = 2 + 3 * 4;     // 14, ne 20
int y = (2 + 3) * 4;   // 20
```

Když si nejsi jistý, **dej závorky** – kód je pak i čitelnější.

**Souvisí:** [[aritmeticke_operatory]], [[prirazeni]], [[inkrement]], [[logicke_operatory]], [[ternarni_operator]]
