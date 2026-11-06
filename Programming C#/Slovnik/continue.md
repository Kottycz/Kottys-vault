---
aliases: [continue]
tags: [slovnik]
---

# continue

**Příkaz, který přeskočí zbytek aktuální iterace [[cyklus|cyklu]] a pokračuje další iterací.**

```csharp
for (int i = 1; i <= 5; i++)
{
    if (i == 3) continue;
    Console.WriteLine(i);   // vypíše 1 2 4 5
}
```

---

## Podrobně

### Jak funguje

Když program narazí na `continue`, **zbytek těla se přeskočí** a cyklus se vrátí k dalšímu průchodu. Cyklus se tedy **neukončí**, jen se jedna iterace „vynechá".

- v [[for]] – skočí na **krok** (`i++`) a pak na podmínku
- v [[while]] a [[do_while]] – skočí rovnou na **kontrolu podmínky**

### Typické použití

Přeskočení prvků, které nechceš zpracovat:

```csharp
// součet jen kladných čísel
int soucet = 0;
foreach (var c in cisla)
{
    if (c <= 0) continue;
    soucet += c;
}
```

### Pozor v cyklu while

U [[while]] se krok nedělá automaticky. Když `i++` napíšeš až **za** `continue`, přeskočí se také a vznikne **nekonečný cyklus**:

```csharp
int i = 0;
while (i < 5)
{
    if (i == 2) continue;   // i se nezvýší → zacyklí se
    i++;
}
```

### break vs. continue

| | [[break]] | continue |
| :-- | :-- | :-- |
| Co ukončí | celý cyklus | jen aktuální iteraci |
| Pokračuje se | příkazem za cyklem | další iterací |

**Souvisí:** [[break]], [[cyklus]], [[for]], [[while]], [[foreach]]
