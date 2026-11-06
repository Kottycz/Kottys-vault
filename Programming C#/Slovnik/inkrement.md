---
aliases: [Inkrement, Dekrement]
tags: [slovnik]
---

# inkrement

**Zvýšení hodnoty o 1** operátorem `++` (dekrement `--` sníží o 1). Záleží, jestli je před proměnnou, nebo za ní.

```csharp
a = 5;
b = a++ - 3;   // b = 2, a = 6
```

---

## Podrobně

### Postfix vs. prefix

| Zápis | Název | Co se stane |
| :-- | :-- | :-- |
| `a++` | postfix | **nejdřív** se použije původní hodnota, **pak** se přičte 1 |
| `++a` | prefix | **nejdřív** se přičte 1, **pak** se použije nová hodnota |

Když stojí `a++` nebo `++a` samostatně na řádku, je to jedno – obojí jen přičte 1. Rozdíl je vidět, až když je součástí výrazu.

### Příklad krok po kroku

```csharp
a = 5;
b = a++ - 3;
// 1. použije se a = 5 → 5 - 3 = 2
// 2. b = 2
// 3. a se zvýší na 6

b = ++a - 3;
// 1. a se zvýší ze 6 na 7
// 2. použije se a = 7 → 7 - 3 = 4
// 3. b = 4
```

### Všechny způsoby, jak přičíst 1

```csharp
a = a + 1;
a += 1;
a++;
++a;
```

Všechny čtyři dělají samostatně totéž.

### Kde se používá

Nejčastěji v cyklech `for`, kde se počítadlo zvyšuje o 1:

```csharp
for (int i = 0; i < 10; i++)
{
    Console.WriteLine(i);
}
```

### Tip

Nepoužívej `++` uvnitř složitějších výrazů – je to nepřehledné a snadno se v tom udělá chyba. Lepší je zvýšit proměnnou na samostatném řádku.

**Souvisí:** [[operator]], [[aritmeticke_operatory]], [[prirazeni]]
