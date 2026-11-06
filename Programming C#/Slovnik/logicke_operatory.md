---
aliases: [Logické operátory, and, or, not]
tags: [slovnik]
---

# logické operátory

**Spojují nebo otáčejí podmínky**: `&&` (a zároveň), `||` (nebo), `!` (negace). Pracují s [[bool]].

```csharp
bool ok = a > 0 && a < 10;
```

---

## Podrobně

### Přehled

| Operátor | Název | True, když… |
| :-- | :-- | :-- |
| `&&` | AND (a zároveň) | platí **obě** strany |
| `\|\|` | OR (nebo) | platí **aspoň jedna** strana |
| `!` | NOT (negace) | otočí hodnotu |

### Pravdivostní tabulka

| A | B | `A && B` | `A \|\| B` | `!A` |
| :-- | :-- | :-- | :-- | :-- |
| true | true | true | true | false |
| true | false | false | true | false |
| false | true | false | true | true |
| false | false | false | false | true |

### Příklady

```csharp
bool vRozsahu = vek >= 15 && vek <= 18;     // 15 až 18
bool vikend = den == 6 || den == 7;         // sobota nebo neděle
bool pracovni = !vikend;                    // opak
```

### Zkrácené vyhodnocení

C# vyhodnocuje zleva a **skončí, jakmile zná výsledek**:

- u `&&` – když je levá strana `false`, pravá se vůbec nevyhodnotí (výsledek je stejně false)
- u `||` – když je levá strana `true`, pravá se nevyhodnotí

Hodí se to na ochranu před chybou:

```csharp
if (b != 0 && a / b > 2)   // když je b = 0, dělení se neprovede
```

### Priorita

`!` má přednost před `&&` a `&&` před `||`. Při kombinaci radši použij závorky:

```csharp
bool x = (a > 0 || b > 0) && c > 0;
```

**Souvisí:** [[bool]], [[operator]], [[ternarni_operator]]
