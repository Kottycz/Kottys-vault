---
aliases: [Index, indexování, indexer]
tags: [slovnik]
---

# index

**Celé číslo, které určuje pozici prvku v poli – píše se do hranatých závorek a počítá se od 0.**

```csharp
int[] a = { 10, 20, 30 };
Console.WriteLine(a[0]);   // 10 (první)
Console.WriteLine(a[2]);   // 30 (poslední)
```

---

## Podrobně

### Číslování od nuly

První prvek má index **0**, druhý 1 atd. Pole o `n` prvcích má platné indexy **0 až n − 1**.

| Pozice | 1. | 2. | 3. |
| :-- | :-- | :-- | :-- |
| Index | `0` | `1` | `2` |
| Hodnota | 10 | 20 | 30 |

Poslední prvek je vždy `a[a.Length - 1]`.

### Index jako proměnná

Index může být libovolný výraz s celočíselným výsledkem – proto se dobře kombinuje s [[for]]:

```csharp
for (int i = 0; i < a.Length; i++)
{
    Console.WriteLine(a[i]);
}
```

### Chyba mimo rozsah

Když použiješ index, který v poli neexistuje (záporný, nebo `>= Length`), program **spadne** s chybou `IndexOutOfRangeException`:

```csharp
int[] a = new int[3];
a[3] = 5;   // CHYBA – platné jsou jen 0, 1, 2
```

Nejčastější příčina: v cyklu `i <= a.Length` místo `i < a.Length`.

### Operátor `[]`

Hranaté závorky jsou v C# samostatný [[operator|operátor]] – **indexování**. Funguje i na řetězci ([[string]] je posloupnost znaků):

```csharp
string jmeno = "Kotty";
char prvni = jmeno[0];   // 'K'
```

### Dvojitý index

U [[dvourozmerne_pole|dvourozměrného pole]] se zadávají dva indexy: `matice[radek, sloupec]`.

**Souvisí:** [[pole]], [[length]], [[for]], [[dvourozmerne_pole]], [[operator]]
