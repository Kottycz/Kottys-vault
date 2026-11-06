---
aliases: [for, cyklus for]
tags: [slovnik]
---

# for

**[[cyklus|Cyklus]] pro známý počet opakování – inicializace, podmínka a krok jsou zapsané na jednom místě.**

```csharp
for (int i = 0; i < 5; i++)
{
    Console.WriteLine(i);   // 0 1 2 3 4
}
```

---

## Podrobně

### Tři části v závorce

```csharp
for (inicializace ; podmínka ; krok)
{
    tělo
}
```

| Část | Kdy se provede | Příklad |
| :-- | :-- | :-- |
| **inicializace** | jednou, na začátku | `int i = 0` |
| **podmínka** | před každou iterací | `i < 5` |
| **krok** | po každé iteraci | `i++` |

### Pořadí provádění

1. inicializace
2. kontrola podmínky → když neplatí, cyklus končí
3. tělo cyklu
4. krok
5. zpět na bod 2

### Krok nemusí být +1

```csharp
for (int i = 10; i > 0; i--) { }    // odpočet 10 → 1
for (int i = 0; i <= 100; i += 10) { }   // po desítkách
```

Zápis kroku je [[inkrement]] nebo [[prirazeni|zkrácené přiřazení]].

### Platnost proměnné

Proměnná `i` deklarovaná v závorce existuje **jen uvnitř cyklu**. Za ním už není.

### Typické použití – průchod polem

```csharp
for (int i = 0; i < cisla.Length; i++)
{
    Console.WriteLine(cisla[i]);
}
```

Podmínka `i < Length` (ne `<=`) – poslední platný [[index]] je o jedna menší než [[length|délka]], jinak vznikne chyba mimo rozsah.

### for vs. foreach

[[for]] má **index** – můžeš prvky měnit a procházet jen část. [[foreach]] je jednodušší, ale index nemá.

**Souvisí:** [[cyklus]], [[while]], [[foreach]], [[pole]], [[index]], [[inkrement]]
