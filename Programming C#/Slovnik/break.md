---
aliases: [break]
tags: [slovnik]
---

# break

**Příkaz, který okamžitě ukončí [[cyklus]] (nebo větev [[switch]]) a program pokračuje příkazem za ním.**

```csharp
for (int i = 0; i < 10; i++)
{
    if (i == 3) break;
    Console.WriteLine(i);   // vypíše 0 1 2
}
```

---

## Podrobně

### Dvě použití

| Kde | Co dělá |
| :-- | :-- |
| v [[cyklus\|cyklu]] | ukončí cyklus, i když podmínka ještě platí |
| ve [[switch]] | ukončí větev `case` (v C# povinné) |

### Jak funguje v cyklu

Program přeruší tělo cyklu **uprostřed** a skočí na první příkaz **za cyklem**. Zbytek těla i zbylé iterace se přeskočí.

### Typické použití

**Hledání:** jakmile prvek najdeš, nemá smysl hledat dál.

```csharp
foreach (var c in cisla)
{
    if (c == 42)
    {
        Console.WriteLine("nalezeno");
        break;
    }
}
```

**Ukončení nekonečného cyklu:**

```csharp
while (true)
{
    string s = Console.ReadLine();
    if (s == "konec") break;
}
```

### Vnořené cykly

`break` ukončí jen **nejbližší** (vnitřní) cyklus. Vnější pokračuje dál.

### break vs. continue

- **break** – končí **celý cyklus**
- [[continue]] – končí jen **aktuální iteraci**, cyklus jede dál

**Souvisí:** [[continue]], [[cyklus]], [[switch]], [[while]], [[for]]
