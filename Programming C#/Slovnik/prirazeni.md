---
aliases: [Přiřazení, Přiřazovací operátory]
tags: [slovnik]
---

# přiřazení

**Uložení hodnoty do proměnné** operátorem `=`. Zkrácené verze `+=`, `-=`… spojí výpočet s uložením.

```csharp
a = 5;
a += 3;   // a = a + 3 → 8
```

---

## Podrobně

### `=` není "rovná se"

V matematice `a = a + 3` nedává smysl, v programování ano: **vpravo se spočítá hodnota, pak se uloží doleva**. Čte se to "a dostane hodnotu a + 3".

Porovnání ("rovná se?") se píše `==` a výsledek je [[bool]]:

```csharp
a = 5;          // přiřazení
bool je = a == 5;   // porovnání → true
```

### Zkrácené přiřazení

| Zápis | Znamená | a = 10 → |
| :-- | :-- | :-- |
| `a += 3` | `a = a + 3` | 13 |
| `a -= 3` | `a = a - 3` | 7 |
| `a *= 3` | `a = a * 3` | 30 |
| `a /= 3` | `a = a / 3` | 3 |
| `a %= 3` | `a = a % 3` | 1 |

Pro přičtení / odečtení jedničky je ještě kratší [[inkrement]] `a++`.

### Směr přiřazení

Vždy **zprava doleva**. Vlevo musí být proměnná, ne výraz:

```csharp
a = b + 1;   // OK
b + 1 = a;   // CHYBA
```

### Kompatibilita typů

Hodnota vpravo musí jít uložit do typu vlevo. Z menšího typu do většího to jde samo, obráceně je potřeba [[pretypovani|přetypování]]:

```csharp
double d = 5;          // OK, int → double
int i = 5.7;           // CHYBA
int i = (int)5.7;      // OK, i = 5
```

**Souvisí:** [[operator]], [[aritmeticke_operatory]], [[inkrement]], [[promenna]], [[pretypovani]]
