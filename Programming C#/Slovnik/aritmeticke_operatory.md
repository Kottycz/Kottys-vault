---
aliases: [Aritmetické operátory, modulo]
tags: [slovnik]
---

# aritmetické operátory

**Základní matematické operace**: `+` sčítání, `-` odčítání, `*` násobení, `/` dělení, `%` zbytek po dělení.

```csharp
int zbytek = 7 % 2;   // 1
```

---

## Podrobně

### Přehled

| Operátor | Význam | Příklad | Výsledek |
| :-- | :-- | :-- | :-- |
| `+` | sčítání | `7 + 2` | 9 |
| `-` | odčítání | `7 - 2` | 5 |
| `*` | násobení | `7 * 2` | 14 |
| `/` | dělení | `7 / 2` | **3** (int) |
| `/` | dělení | `7.0 / 2` | 3.5 |
| `%` | zbytek (modulo) | `7 % 2` | 1 |

### Dělení `/`

Záleží na typech: dva [[int|inty]] dají int (desetinná část se zahodí), jakmile je aspoň jeden desetinný, dá výsledek [[double]]. Viz [[celociselne_deleni|celočíselné dělení]].

Dělení nulou:
- u intů → program **spadne** (`DivideByZeroException`)
- u doublu → výsledek `Infinity`, program jede dál

### Modulo `%`

Vrací **zbytek po celočíselném dělení**. Typické použití:

```csharp
bool sude = x % 2 == 0;       // je číslo sudé?
int posledniCislice = x % 10; // 1234 % 10 = 4
int sekundy = 125 % 60;       // 5 (125 s = 2 min 5 s)
```

### Mocnina

C# **nemá** operátor na mocninu – `^` znamená něco jiného (XOR). Mocnina se dělá přes [[math|Math.Pow]]:

```csharp
double m = Math.Pow(2, 3);   // 8
```

### Zkrácené zápisy

`a = a + 3` jde zapsat jako `a += 3` – viz [[prirazeni|přiřazení]]. Přičtení jedničky jako `a++` – viz [[inkrement]].

**Souvisí:** [[operator]], [[celociselne_deleni]], [[prirazeni]], [[inkrement]], [[math]]
