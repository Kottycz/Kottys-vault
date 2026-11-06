---
aliases: [while, cyklus while]
tags: [slovnik]
---

# while

**[[cyklus|Cyklus]] s podmínkou na začátku – tělo se opakuje, dokud je podmínka splněná.**

```csharp
int i = 0;
while (i < 5)
{
    Console.WriteLine(i);
    i++;
}
```

---

## Podrobně

### Jak funguje

1. zkontroluje se [[podminka|podmínka]]
2. platí → provede se tělo a vrátí se na bod 1
3. neplatí → cyklus končí

Protože se podmínka testuje **před** tělem, může cyklus proběhnout i **nula krát** (když neplatí hned na začátku).

### Kdy použít

Když předem **nevíš, kolikrát** se bude opakovat – závisí to na něčem, co se děje za běhu.

```csharp
// opakuj, dokud uživatel nezadá platné číslo
int a;
while (!int.TryParse(Console.ReadLine(), out a))
{
    Console.Write("Zadej číslo znovu: ");
}
```

### Pozor na nekonečný cyklus

V těle se musí něco měnit, aby podmínka jednou přestala platit. Zapomenuté `i++` v příkladu výše = program nikdy neskončí.

### while (true)

Záměrně nekonečný cyklus, který se ukončí příkazem [[break]]:

```csharp
while (true)
{
    string s = Console.ReadLine();
    if (s == "konec") break;
}
```

### while vs. for

- [[for]] – počet opakování je jasný (počítadlo)
- **while** – opakuje se „dokud…"

### while vs. do while

U [[do_while]] se podmínka kontroluje až na konci, takže tělo proběhne **vždy aspoň jednou**.

**Souvisí:** [[cyklus]], [[for]], [[do_while]], [[break]], [[podminka]]
