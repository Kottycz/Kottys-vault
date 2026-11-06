---
aliases: [Implicitní konverze, implicitní převod, automatická konverze]
tags: [slovnik]
---

# implicitní konverze

**Automatický převod jednoho typu na jiný, který provede kompilátor sám – bez zápisu přetypování.**

```csharp
int a = 5;
double d = a;                       // int → double sám
Console.WriteLine("a = " + a);      // číslo → text sám
```

---

## Podrobně

### Dva hlavní případy

**1. Číselné typy – menší do většího**

Kompilátor převede sám, když se **nic neztratí**:

```
byte → short → int → long → float → double
```

```csharp
int i = 5;
long l = i;      // OK
double d = i;    // OK
```

Opačným směrem (třeba `double` → `int`) by se ztratila desetinná část, proto je potřeba výslovné [[pretypovani|přetypování]].

**2. Výpis do konzole**

Při výpisu se číslo automaticky převede na text, takže ho není třeba převádět ručně:

```csharp
Console.WriteLine("Součet je " + 7);          // Součet je 7
Console.WriteLine($"Součet je {7}");          // totéž
```

V učivu: *„u výpisu probíhá implicitní konverze čísla na string, není třeba ho konvertovat."* Viz [[vypis_promennych]].

### Implicitní × explicitní

| | Implicitní | Explicitní |
| :-- | :-- | :-- |
| Kdo ji provede | kompilátor | programátor |
| Zápis | žádný | `(typ)hodnota` |
| Ztráta dat | ne | může nastat |
| Příklad | `double d = 5;` | `int i = (int)5.7;` |

### Co nejde ani implicitně, ani přetypováním

[[string|Text]] na číslo – na to je potřeba [[parse|Parse]]:

```csharp
int a = int.Parse("5");   // (int)"5" nejde
```

### Pozor při spojování

Jakmile je vlevo text, `+` už čísla **nesčítá**, ale lepí jako text:

```csharp
Console.WriteLine("součet: " + 2 + 3);     // součet: 23
Console.WriteLine("součet: " + (2 + 3));   // součet: 5
```

**Souvisí:** [[pretypovani]], [[parse]], [[vypis_promennych]], [[datovy_typ]], [[string]], [[writeline]]
