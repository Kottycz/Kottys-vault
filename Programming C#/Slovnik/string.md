---
aliases: [string, řetězec, String]
tags: [slovnik]
---

# string

**Řetězec** – text libovolné délky (i prázdný). Píše se do **dvojitých** uvozovek.

```csharp
string jmeno = "Kotty";
```

---

## Podrobně

### Vlastnosti

- Řetězec je složený z jednotlivých [[char|znaků]], indexují se od 0: `jmeno[0]` je `'K'`.
- Délka: `jmeno.Length` → 5
- Prázdný řetězec: `""` nebo `string.Empty`
- Výchozí hodnota: `null` (žádný řetězec) – to není totéž co `""`.

### Spojování

Řetězce se spojují operátorem `+`. Když spojíš string s číslem, číslo se automaticky převede na text:

```csharp
string s = "Ahoj " + jmeno;        // "Ahoj Kotty"
string t = "a = " + 5;              // "a = 5"
string u = "1" + 2 + 3;             // "123" (ne 6!)
```

Přehlednější je interpolace – viz [[vypis_promennych|výpis proměnných]]:

```csharp
string s = $"Ahoj {jmeno}";
```

### Nejde změnit (immutable)

String se po vytvoření nedá upravit. Každá "změna" ve skutečnosti vytvoří nový řetězec. U spojování v cyklu (tisíce opakování) je to pomalé – tam se používá `StringBuilder`.

### Užitečné metody

| Metoda | Co dělá | Příklad |
| :-- | :-- | :-- |
| `ToUpper()` | velká písmena | `"ahoj".ToUpper()` → `"AHOJ"` |
| `ToLower()` | malá písmena | `"AHOJ".ToLower()` → `"ahoj"` |
| `Trim()` | ořízne mezery na krajích | `" a ".Trim()` → `"a"` |
| `Contains(x)` | obsahuje x? | `"Kotty".Contains("ott")` → `true` |
| `Replace(a, b)` | nahradí a za b | `"a-b".Replace("-", "+")` → `"a+b"` |

### Vstup z konzole

[[readline|Console.ReadLine()]] vrací vždy string – i když uživatel napíše číslo. Na číslo se převede přes [[parse|Parse]].

**Souvisí:** [[datovy_typ]], [[char]], [[vypis_promennych]], [[escape_sekvence]], [[readline]], [[parse]]
