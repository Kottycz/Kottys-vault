---
aliases: [Array, Array.Sort, Array.Reverse, Array.Copy]
tags: [slovnik]
---

# Array

**Vestavěná třída s užitečnými metodami pro práci s [[pole|poli]] – třídění, obrácení pořadí a kopírování.**

```csharp
int[] a = { 5, 2, 9, 1 };
Array.Sort(a);      // 1 2 5 9
Array.Reverse(a);   // 9 5 2 1
```

---

## Podrobně

### Metody z učiva

| Metoda | Co dělá |
| :-- | :-- |
| `Array.Sort(pole)` | **setřídí** pole vzestupně |
| `Array.Reverse(pole)` | **obrátí pořadí** prvků (pozpátku) |
| `Array.Copy(původní, nové, počet)` | **zkopíruje** zadaný počet prvků do jiného pole |

### Měnící se původní pole

`Sort` i `Reverse` pracují **přímo s polem** – původní pořadí se ztratí. Chceš-li si ho ponechat, nejdřív pole zkopíruj.

### Sort + Reverse = sestupně

`Sort` řadí od nejmenšího. Na sestupné pořadí se po něm zavolá `Reverse`:

```csharp
Array.Sort(a);
Array.Reverse(a);   // od největšího
```

Řadí se i [[string|řetězce]] (abecedně).

### Array.Copy

Cílové pole **musí už existovat** a být dost velké:

```csharp
int[] puvodni = { 1, 2, 3, 4 };
int[] kopie = new int[4];
Array.Copy(puvodni, kopie, 4);   // kopie je nezávislé pole
```

### Proč ne `b = a`

Pole je [[referencni_typ|referenční typ]]. `b = a` nevytvoří kopii – obě proměnné pak ukazují na **totéž pole** a změna přes jednu je vidět i přes druhou. Skutečnou kopii udělá až `Array.Copy`.

```csharp
int[] a = { 1, 2, 3 };
int[] b = a;       // totéž pole
b[0] = 99;         // a[0] je teď také 99
```

### Další užitečné

- `Array.IndexOf(pole, hodnota)` – najde pozici prvku (nebo vrátí −1)
- `Array.Clear(pole)` – vynuluje prvky

**Souvisí:** [[pole]], [[length]], [[index]], [[referencni_typ]], [[math]]
