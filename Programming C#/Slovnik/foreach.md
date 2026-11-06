---
aliases: [foreach, cyklus foreach]
tags: [slovnik]
---

# foreach

**[[cyklus|Cyklus]], který projde všechny prvky [[pole]] nebo [[kolekce]] – délku si zjistí sám.**

```csharp
foreach (var jmeno in studenti)
{
    Console.WriteLine(jmeno);
}
```

---

## Podrobně

### Zápis

```csharp
foreach (datovýTyp proměnná in kolekce)
{
    // práce s proměnnou
}
```

V každé iteraci dostane `proměnná` **další prvek** kolekce – od prvního po poslední.

### Výhody

- **jednoduchý zápis** – žádné počítadlo, žádný [[index]]
- **sám zjistí délku** – nehrozí chyba mimo rozsah
- čitelný: „pro každé jméno ve studentech…"

### Omezení

- **nemá řídící proměnnou (index)** – nevíš, kolikátý prvek zrovna zpracováváš
- proto se **nehodí na naplňování pole** – jen na čtení
- **nelze měnit proměnnou cyklu** – `jmeno = "X"` je chyba
- prochází vždy **celou** kolekci od začátku (zastavit jde jen přes [[break]])
- u seznamů nelze během průchodu přidávat ani odebírat prvky

### Typ proměnné

Místo konkrétního typu jde použít [[var]] – kompilátor si typ odvodí z kolekce:

```csharp
int[] cisla = { 4, 8, 15 };
foreach (var c in cisla)      // c je int
{
    Console.WriteLine(c * 2);
}
```

### foreach vs. for

| | foreach | [[for]] |
| :-- | :-- | :-- |
| Index | ne | ano |
| Čtení všech prvků | ✔ nejjednodušší | ✔ |
| Změna prvků pole | ✘ | ✔ |
| Procházení jen části | ✘ | ✔ |
| Pozpátku | ✘ | ✔ |

### K čemu ho použít

Na výpis, součet, hledání maxima – všude, kde potřebuješ každý prvek **jen přečíst**.

**Souvisí:** [[cyklus]], [[for]], [[pole]], [[kolekce]], [[var]], [[break]]
