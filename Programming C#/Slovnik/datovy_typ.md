---
aliases: [Datový typ, Datové typy]
tags: [slovnik]
---

# datový typ

Určuje, **jaký druh hodnoty** [[promenna|proměnná]] uchovává a kolik zabírá paměti.

```csharp
int a = 1;   // int = datový typ
```

---

## Podrobně

### Proč typy existují

C# je **staticky typovaný** jazyk – typ proměnné se určí při deklaraci a už se nezmění. Kompilátor tak odhalí chyby dřív, než se program spustí (třeba když se snažíš uložit text do čísla).

```csharp
int a = 5;
a = "ahoj";   // CHYBA – do intu nejde uložit string
```

### Základní typy

| Typ | Co uchovává | Příklad | Velikost |
| :-- | :-- | :-- | :-- |
| [[int]] | celé číslo | `5` | 32 b |
| [[float]] | desetinné číslo (jednoduchá přesnost) | `6.4f` | 32 b |
| [[double]] | desetinné číslo (dvojitá přesnost) | `5.6` | 64 b |
| [[decimal]] | desetinné číslo s nejvyšší přesností (peníze) | `5.6m` | 128 b |
| [[char]] | jeden znak | `'A'` | 16 b |
| [[string]] | text | `"A"` | proměnná |
| [[bool]] | pravda / nepravda | `true` | 8 b |

### Hodnotové a referenční typy

Typy se dělí podle toho, co je uloženo v proměnné:

- [[hodnotovy_typ|hodnotové]] – přímo hodnota ([[int]], [[double]], [[bool]], [[char]])
- [[referencni_typ|referenční]] – odkaz na data ([[string]], [[pole]], `object`) – mohou být [[null]]

### Převody mezi typy

- **Automaticky (implicitně)** – z menšího typu do většího, kde se nic neztratí: `int` → `double` – viz [[implicitni_konverze]]
- **Ručně ([[pretypovani|přetypování]])** – z většího do menšího, kde se může něco ztratit: `(int)3.7` → 3
- **Z textu** – přes [[parse|Parse]]: `int.Parse("5")`

### var

Místo typu jde napsat [[var]] – kompilátor si typ odvodí sám z hodnoty. Typ je ale pořád pevný:

```csharp
var x = 5;     // x je int
var y = 5.0;   // y je double
```

**Souvisí:** [[promenna]], [[int]], [[float]], [[double]], [[char]], [[string]], [[bool]], [[pretypovani]]
