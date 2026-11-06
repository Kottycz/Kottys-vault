---
aliases: [Hodnotový typ, hodnotové typy, value type]
tags: [slovnik]
---

# hodnotový typ

**Typ, jehož proměnná obsahuje přímo samotnou hodnotu (číslo, znak, logickou hodnotu).**

```csharp
int a = 5;
int b = a;   // b dostane vlastní kopii hodnoty
b = 9;       // a zůstává 5
```

---

## Podrobně

### Co sem patří

| Skupina | Typy |
| :-- | :-- |
| celočíselné | [[int]], `long`, `short`, `byte` |
| s desetinnou čárkou | [[float]], [[double]] |
| s vyšší přesností | [[decimal]] |
| logický | [[bool]] |
| znak | [[char]] |

### Kopírování

Při přiřazení se **hodnota zkopíruje**. Obě proměnné jsou pak na sobě nezávislé – změna jedné druhou neovlivní.

### Nikdy nejsou null

Hodnotová proměnná **vždy něco obsahuje** – číslo má aspoň 0, [[bool]] má `false`. Hodnotu [[null]] mít nemůže.

### Hodnotový × referenční typ

| | hodnotový | [[referencni_typ\|referenční]] |
| :-- | :-- | :-- |
| V proměnné je | **hodnota** | **odkaz** na data |
| Přiřazení `b = a` | vznikne kopie | oba ukazují na totéž |
| Může být [[null]] | ne | ano |
| Příklady | [[int]], [[double]], [[bool]], [[char]] | [[string]], [[pole]], `object` |

### Předávání do metod

Do metody se hodnotový typ normálně předá **kopií** – metoda původní proměnnou nezmění. Aby ji změnila, musí se použít [[ref]].

**Souvisí:** [[referencni_typ]], [[datovy_typ]], [[int]], [[double]], [[bool]], [[null]], [[ref]]
