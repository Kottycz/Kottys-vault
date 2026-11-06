---
aliases: [namespace, jmenný prostor]
tags: [slovnik]
---

# namespace

**Jmenný prostor** – "složka" pro kód, seskupuje [[trida|třídy]] a zabraňuje konfliktům stejných jmen.

```csharp
namespace uvod
{
    // třídy
}
```

---

## Podrobně

### K čemu je

Ve velkých projektech a knihovnách můžou existovat dvě třídy se stejným jménem (třeba `Program`). Namespace je odliší – plné jméno pak je `uvod.Program` vs. `jinyProjekt.Program`. Funguje to podobně jako složky na disku: dva soubory se stejným jménem můžou být ve dvou různých složkách.

### Vnořování

Namespace se dají vnořovat, části se oddělují tečkou:

```csharp
namespace Skola.Programovani.Uvod
{
}
```

### using

`Console` a `Math` jsou ve skutečnosti v namespace `System` – plně by se psalo `System.Console.WriteLine()`. Aby se to nemuselo psát pokaždé, dává se na začátek souboru `using`:

```csharp
using System;

Console.WriteLine("ahoj");   // místo System.Console.WriteLine
```

V nových verzích .NET se nejběžnější `using` přidávají automaticky (implicit usings), proto je v tvém kódu nevidíš.

### Zkrácený zápis

Od C# 10 jde napsat namespace bez složených závorek – platí pak pro celý soubor:

```csharp
namespace uvod;
```

**Souvisí:** [[trida]], [[main]]
