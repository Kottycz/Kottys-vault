---
aliases: [Ternární operátor]
tags: [slovnik]
---

# ternární operátor

**Zkrácená podmínka na jeden řádek**: `podminka ? kdyz_true : kdyz_false`.

```csharp
b = a > 5 ? 1 : 2;   // a > 5 → b = 1, jinak b = 2
```

---

## Podrobně

### Jak se čte

```
a > 5  ?  1  :  2
  │       │     └── hodnota, když podmínka neplatí
  │       └──────── hodnota, když podmínka platí
  └──────────────── podmínka (výsledek je bool)
```

"Je a větší než 5? Pokud ano, 1. Pokud ne, 2."

### Stejné jako if/else

```csharp
// ternární operátor
b = a > 5 ? 1 : 2;

// totéž přes if/else
if (a > 5)
{
    b = 1;
}
else
{
    b = 2;
}
```

### Častá chyba

Ternární operátor **vrací hodnotu**, nedělá příkazy. Přiřazení patří **před** podmínku:

```csharp
a > 5 ? b = 1 : b = 2;   // CHYBA – nejde zkompilovat
b = a > 5 ? 1 : 2;        // OK
```

### Praktické příklady

```csharp
string stav = vek >= 18 ? "dospělý" : "nezletilý";
int max = a > b ? a : b;
Console.WriteLine(x % 2 == 0 ? "sudé" : "liché");
```

### Kdy ho nepoužívat

Na jednoduchý výběr mezi dvěma hodnotami je ideální. Když se začne vnořovat (`a ? b : c ? d : e`), je to nečitelné – tam je lepší klasický `if`.

**Souvisí:** [[operator]], [[bool]], [[logicke_operatory]]
