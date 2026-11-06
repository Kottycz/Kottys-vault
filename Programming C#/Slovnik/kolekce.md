---
aliases: [Kolekce, seznam, list, List]
tags: [slovnik]
---

# kolekce

**Obecný název pro strukturu, která drží víc prvků pohromadě – například [[pole]] nebo seznam (`List<T>`).**

```csharp
List<string> studenti = new List<string>();
studenti.Add("Petr");
studenti.Add("Jana");
```

---

## Podrobně

### Co je kolekce

Cokoliv, co v sobě drží **víc hodnot** a dá se procházet. Cyklus [[foreach]] umí projít libovolnou kolekci – v učivu se označuje `list` („seznam, pole, atd.").

### Pole × seznam

| | [[pole]] | seznam `List<T>` |
| :-- | :-- | :-- |
| Velikost | **pevná** (po vytvoření nejde změnit) | **proměnlivá** (roste podle potřeby) |
| Počet prvků | [[length\|Length]] | `Count` |
| Přidání prvku | nejde | `Add(prvek)` |
| Odebrání prvku | nejde | `Remove(prvek)` |
| Přístup k prvku | `a[0]` | `seznam[0]` |

### Seznam

`List<T>` – `T` je typ prvků (`int`, `string`, …):

```csharp
List<int> cisla = new List<int>();
cisla.Add(5);
cisla.Add(8);
Console.WriteLine(cisla.Count);   // 2
Console.WriteLine(cisla[0]);      // 5
```

Prvky mají [[index|indexy]] stejně jako v poli – od 0.

### Procházení

```csharp
foreach (var s in studenti)
{
    Console.WriteLine(s);
}
```

Obě struktury se dají procházet i přes [[for]] (u seznamu se používá `Count` místo `Length`).

### Kdy co

- **pole** – počet prvků předem znám a nemění se
- **seznam** – počet se mění (načítání dat, přidávání položek)

### Další kolekce

`Dictionary` (slovník – dvojice klíč/hodnota), `Queue` (fronta), `Stack` (zásobník).

**Souvisí:** [[pole]], [[foreach]], [[for]], [[length]], [[index]], [[cyklus]]
