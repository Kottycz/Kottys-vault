---
aliases: [Proměnná, Proměnné]
tags: [slovnik]
---

# proměnná

**Pojmenované místo v paměti**, kam se ukládá hodnota, která se může během programu měnit.

```csharp
int a = 1;
a = 5;   // změna hodnoty
```

---

## Podrobně

### Deklarace a inicializace

- **Deklarace** – vytvoření proměnné: řekneš typ a jméno
- **Inicializace** – první přiřazení hodnoty

```csharp
float b;       // deklarace
b = 6.4f;      // inicializace
int a = 1;     // obojí najednou
int x, y, z;   // víc proměnných stejného typu najednou
```

Proměnnou nejde použít, dokud nemá hodnotu – kompilátor to ohlásí jako chybu.

### Pravidla pro jména

- smí obsahovat písmena, číslice a `_`
- **nesmí začínat číslicí** (`1a` ne, `a1` ano)
- nesmí to být klíčové slovo (`int`, `class`, `if`…)
- **rozlišují se velká a malá písmena** – `vek` a `Vek` jsou dvě různé proměnné

Zvyk v C#: lokální proměnné se píšou **camelCase** – `pocetZaku`, `obsahTrojuhelniku`.

### Platnost (scope)

Proměnná platí jen v bloku `{ }`, kde byla deklarovaná. Mimo něj neexistuje:

```csharp
if (a > 5)
{
    int x = 10;
}
Console.WriteLine(x);   // CHYBA – x tady neexistuje
```

### Proměnná vs. konstanta

| | Proměnná | [[konstanta|Konstanta]] |
| :-- | :-- | :-- |
| Změna hodnoty | ano | ne |
| Zápis | `int a = 5;` | `const int g = 5;` |

**Souvisí:** [[datovy_typ]], [[konstanta]], [[prirazeni]]
