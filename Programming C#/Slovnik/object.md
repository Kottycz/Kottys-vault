---
aliases: [object]
tags: [slovnik]
---

# object

**Nadřazený [[referencni_typ|referenční typ]], do kterého jde uložit hodnotu jakéhokoliv jiného typu.**

```csharp
object o = 5;
o = "text";
o = 3.14;      // do objectu jde cokoliv
```

---

## Podrobně

### Základ všech typů

Všechny typy v C# – i [[int]], [[string]] nebo [[pole]] – od `object` nepřímo **dědí**. Proto se do proměnné typu `object` vejde cokoliv.

### Rozdíl oproti var

| | `object` | [[var]] |
| :-- | :-- | :-- |
| Typ proměnné | vždy `object` | odvodí se z hodnoty |
| Změna typu hodnoty | **jde** (`o = 5; o = "a";`) | nejde |

### Nevýhoda

S hodnotou v `object` se **nedá přímo počítat**. Musí se převést zpět:

```csharp
object o = 5;
int a = (int)o;      // zpětné přetypování
int b = o + 1;       // CHYBA
```

Převod na nesprávný typ způsobí chybu za běhu (`InvalidCastException`).

### Boxing

Když se [[hodnotovy_typ|hodnotový typ]] (např. [[int]]) uloží do `objectu`, zabalí se do „krabičky" v paměti – tomu se říká **boxing**. Je to pomalejší.

### Kdy se používá

Dnes spíš výjimečně – existují lepší řešení (generika, `List<T>`). Hodí se tam, kde opravdu nevíš, jaký typ přijde.

### Užitečná metoda

Každý objekt má metodu `ToString()`, která ho převede na text – díky ní [[writeline|WriteLine]] vypíše cokoliv. Viz [[implicitni_konverze]].

**Souvisí:** [[referencni_typ]], [[var]], [[pretypovani]], [[hodnotovy_typ]], [[datovy_typ]]
