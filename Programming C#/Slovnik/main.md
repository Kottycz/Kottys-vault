---
aliases: [Main, metoda Main]
tags: [slovnik]
---

# Main

**Vstupní bod programu** – metoda, která se spustí jako první. Program běží, dokud Main neskončí.

```csharp
static void Main(string[] args)
{
    Console.WriteLine("Program začíná tady");
}
```

---

## Podrobně

### Rozbor hlavičky

```csharp
static void Main(string[] args)
```

| Část | Význam |
| :-- | :-- |
| `static` | metoda patří přímo [[trida|třídě]] – nemusí se vytvářet objekt, aby šla spustit |
| `void` | metoda nic nevrací |
| `Main` | jméno – podle něj systém pozná, kde program začíná |
| `string[] args` | pole textů – parametry předané při spuštění z příkazové řádky |

### Pravidla

- v programu musí být **právě jedna** metoda Main
- musí se jmenovat přesně `Main` (velké M)
- musí být `static`

### args

Když se program spustí z příkazové řádky s parametry, dostane je v `args`:

```
uvod.exe ahoj 5
```

```csharp
Console.WriteLine(args[0]);   // ahoj
Console.WriteLine(args[1]);   // 5
```

Při spuštění z Visual Studia je `args` prázdné.

### Top-level statements

V nových projektech (.NET 6+) může Visual Studio vytvořit soubor bez `namespace`, `class` i `Main` – jen samotný kód:

```csharp
Console.WriteLine("Hello, World!");
```

Main tam pořád existuje, jen ho kompilátor doplní sám "za scénou". Ve škole používáte plný zápis, aby byla vidět struktura.

**Souvisí:** [[trida]], [[namespace]], [[komentar]]
