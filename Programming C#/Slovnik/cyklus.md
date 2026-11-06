---
aliases: [Cyklus, cykly, iterace, smyčka, loop]
tags: [slovnik]
---

# cyklus

**Opakování bloku příkazů – kód se provádí znovu a znovu, dokud platí podmínka.**

```csharp
for (int i = 0; i < 3; i++)
{
    Console.WriteLine("ahoj");   // vypíše se 3×
}
```

---

## Podrobně

### Proč cykly existují

Kdyby sis měl vypsat čísla od 1 do 100, bez cyklu bys musel napsat 100 řádků. Cyklus je napíše na tři.

### Iterace

Jeden průchod tělem cyklu se nazývá **iterace**. Cyklus, který proběhne třikrát, má tři iterace.

### Druhy cyklů

| Cyklus | Kdy použít | Podmínka se testuje |
| :-- | :-- | :-- |
| [[for]] | **znám počet** opakování | na začátku |
| [[while]] | neznám počet, může proběhnout i **nula** krát | na začátku |
| [[do_while]] | neznám počet, musí proběhnout **aspoň jednou** | na konci |
| [[foreach]] | procházím všechny prvky [[pole]] nebo [[kolekce]] | – (projde vše) |

### Řízení cyklu

- [[break]] – cyklus **úplně ukončí**
- [[continue]] – přeskočí zbytek **aktuální iterace** a jde na další

### Nekonečný cyklus

Když podmínka nikdy nepřestane platit, cyklus nikdy neskončí – program „zamrzne".

```csharp
while (true)
{
    // běží do nekonečna – ukončí ho jen break
}
```

Nejčastější příčina chyby: v těle se **nezmění** proměnná, kterou podmínka kontroluje (zapomenuté `i++`).

### Vnořené cykly

Cyklus uvnitř cyklu – vnitřní proběhne celý při každé iteraci vnějšího. Typické pro [[dvourozmerne_pole|dvourozměrná pole]] (řádky × sloupce).

**Souvisí:** [[for]], [[while]], [[do_while]], [[foreach]], [[break]], [[continue]], [[podminka]], [[pole]]
