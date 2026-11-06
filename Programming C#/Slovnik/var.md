---
aliases: [var]
tags: [slovnik]
---

# var

**Klíčové slovo, díky kterému si kompilátor sám odvodí typ proměnné z přiřazené hodnoty.**

```csharp
var x = 5;        // int
var y = 5.0;      // double
var s = "ahoj";   // string
```

---

## Podrobně

### Jak funguje

Místo [[datovy_typ|typu]] napíšeš `var`. Kompilátor se podívá na hodnotu **vpravo** a typ doplní sám. Výsledek je stejný, jako kdyby sis typ napsal ručně.

### Typ je pořád pevný

`var` **není** „libovolný typ". Po odvození se typ už nezmění:

```csharp
var x = 5;
x = "text";   // CHYBA – x je int
```

### Pravidla

- proměnná musí být při deklaraci **rovnou inicializovaná**: `var x;` nejde
- nejde dát jako [[null]]: `var x = null;` nejde (kompilátor nepozná typ)
- funguje jen u **lokálních proměnných** (uvnitř metody)

### Kdy se hodí

Nejčastěji ve [[foreach]], kde se typ prvků odvodí z kolekce:

```csharp
foreach (var jmeno in studenti)
{
    Console.WriteLine(jmeno);
}
```

Hodí se i u dlouhých názvů typů, kde `var` zkrátí zápis.

### Pozor na čitelnost

Když z hodnoty není vidět typ, je lepší ho napsat výslovně:

```csharp
var x = Spocitej();     // jaký typ? není vidět
int x = Spocitej();     // jasné
```

### Desetinná čísla

`var y = 5.6;` je [[double]], ne [[float]] – `float` by potřeboval `5.6f`.

**Souvisí:** [[datovy_typ]], [[promenna]], [[foreach]], [[null]]
