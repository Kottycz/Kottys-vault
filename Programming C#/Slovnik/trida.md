---
aliases: [class, Třída]
tags: [slovnik]
---

# třída

**Základní stavební blok programu v C#** (`class`) – obsahuje metody (co umí) a data (co si pamatuje).

```csharp
internal class Program
{
    static void Main(string[] args) { }
}
```

---

## Podrobně

### Třída jako šablona

Třída je **předpis** – popisuje, jak má něco vypadat a co umí. Podle ní se pak vytvářejí konkrétní **objekty**. Jako plánek domu (třída) a skutečné domy postavené podle něj (objekty).

```csharp
class Pes
{
    public string Jmeno;
    public void Stekni() { Console.WriteLine("Haf!"); }
}

Pes rex = new Pes();   // objekt podle třídy
rex.Jmeno = "Rex";
rex.Stekni();
```

Tohle je základ **objektově orientovaného programování** – přijde později.

### Třída Program

Zatím pracuješ jen s jednou třídou `Program`, která obsahuje metodu [[main|Main]]. Je to jen "obal", protože v C# musí být všechen kód uvnitř nějaké třídy.

### Modifikátory přístupu

Určují, kdo třídu nebo její části vidí:

| Modifikátor | Kdo to vidí |
| :-- | :-- |
| `public` | kdokoliv |
| `internal` | jen kód ve stejném projektu (výchozí pro třídy) |
| `private` | jen uvnitř třídy (výchozí pro členy třídy) |

### Vestavěné třídy

Běžně používáš třídy, které už někdo napsal: `Console` ([[konzole]]), [[math|Math]], `String`. Jejich metody se volají přes tečku: `Math.Sqrt(2)`.

**Souvisí:** [[namespace]], [[main]], [[konzole]], [[math]]
