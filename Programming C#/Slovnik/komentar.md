---
aliases: [Komentář, Komentáře]
tags: [slovnik]
---

# komentář

**Text v kódu, který se neprovádí** – poznámka pro člověka. `//` jednořádkový, `/* */` víceřádkový.

```csharp
int a = 1; // deklarace proměnné a
```

---

## Podrobně

### Druhy

```csharp
// jednořádkový – platí od // do konce řádku

/*
   víceřádkový –
   platí od /* až po */
*/

/// <summary>
/// dokumentační – popisuje metodu, Visual Studio ho pak ukazuje v nápovědě
/// </summary>
```

### Zakomentování kódu

Komentář se často používá na dočasné "vypnutí" kódu – program ho přeskočí, ale kód zůstane v souboru:

```csharp
/*
int a = 1;
Console.WriteLine(a);
*/
```

Ve Visual Studiu: označit řádky → **Ctrl+K, Ctrl+C** (zakomentovat), **Ctrl+K, Ctrl+U** (odkomentovat).

### Pozor na neuzavřený `/*`

Když chybí `*/`, zakomentuje se všechno až do konce souboru a kód přestane fungovat.

### Jak psát dobré komentáře

- vysvětluj **proč**, ne **co** – co kód dělá, je vidět z kódu
- nekomentuj samozřejmosti

```csharp
a = a + 1;       // přičte 1 k a        ← zbytečné
d = 3.0 / 4;     // .0 kvůli celočíselnému dělení  ← užitečné
```

**Souvisí:** [[main]], [[trida]]
