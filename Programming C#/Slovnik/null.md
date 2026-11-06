---
aliases: [null, NullReferenceException]
tags: [slovnik]
---

# null

**Speciální hodnota [[referencni_typ|referenčních typů]], která znamená, že reference neukazuje na žádná data.**

```csharp
string jmeno = null;   // proměnná existuje, ale text neexistuje
```

---

## Podrobně

### Co znamená

Referenční proměnná je „lístek s adresou" – `null` je lístek, na kterém **adresa není**. Proměnná nikam neukazuje.

### Kdo může být null

| Typ | Může být null? |
| :-- | :-- |
| [[referencni_typ\|referenční]] ([[string]], [[pole]], …) | ano |
| [[hodnotovy_typ\|hodnotový]] ([[int]], [[bool]], …) | **ne** (číslo má vždy nějakou hodnotu) |

### null × prázdný řetězec × nula

Tři různé věci:

- `string s = null;` – řetězec **neexistuje**
- `string s = "";` – řetězec existuje, je **prázdný**
- `int a = 0;` – obyčejné číslo nula

### Nejčastější chyba

Zavoláš něco na `null` a program spadne s chybou **`NullReferenceException`**:

```csharp
string s = null;
Console.WriteLine(s.Length);   // CHYBA – není na čem zjistit délku
```

Totéž u pole, které se zapomnělo vytvořit:

```csharp
int[] a;           // jen deklarace
a[0] = 5;          // CHYBA – pole neexistuje (chybí new int[...])
```

### Ošetření

```csharp
if (s != null)
{
    Console.WriteLine(s.Length);
}
```

nebo zkráceně `s?.Length` (vrátí null, když je `s` null).

### Proč je to užitečné

`null` umožňuje říct „tady zatím nic není" – třeba hledání prvku, který se nenašel.

**Souvisí:** [[referencni_typ]], [[hodnotovy_typ]], [[pole]], [[string]], [[ref]]
