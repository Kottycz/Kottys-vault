---
aliases: [Opakování 4, Cykly, Cyklus]
tags: [opakovani, csharp]
---

# 04 – Cykly

Opakování k testu. [[cyklus|Cyklus]] opakuje blok příkazů, dokud platí podmínka.

## Přehled

| Cyklus | Kdy použít |
| :-- | :-- |
| [[for]] | znám počet opakování |
| [[while]] | neznám počet, podmínka se testuje **na začátku** |
| [[do_while\|do while]] | neznám počet, tělo proběhne **aspoň jednou** |
| [[foreach]] | procházím pole nebo seznam |

## for

```csharp
for (inicializace ; podmínka ; krok)
{
   tělo
}
```

Cyklus pro **známý počet opakování**:

- **inicializace** – deklarace proměnné cyklu + její počátek
- **podmínka** – do kdy cyklus probíhá
- **krok** – po kolika bude cyklus přičítat nebo odčítat (viz [[inkrement]])

```csharp
for (int i = 0; i < 10; i++)
{
   Console.WriteLine(i);
}
```

## while

```csharp
while (podmínka)
{
   tělo cyklu
}
```

Cyklus s **podmínkou na začátku**. Probíhá tak dlouho, dokud je podmínka splněna. Když podmínka neplatí hned na začátku, tělo se neprovede ani jednou.

## do while

```csharp
do
{
   tělo cyklu
}
while (podmínka);
```

Cyklus s **podmínkou na konci** – tělo se vždy provede **aspoň jednou**. Za `while` se píše středník.

## break a continue

| Příkaz | Co udělá |
| :-- | :-- |
| [[break]] | ukončí cyklus z jeho těla, pokračuje se příkazem **za cyklem** |
| [[continue]] | přeskočí zbytek těla aktuální iterace, pokračuje se **další iterací** |

## foreach

```csharp
foreach (var proměnná in list)
{
   práce s proměnnou
}
```

- prochází **všechny prvky** pole nebo seznamu
- **sám si zjistí délku** pole nebo seznamu
- `var` – kompilátor si sám odvodí typ proměnné (viz [[var]])
- `list` – seznam, pole atd. (viz [[kolekce]], [[pole]])

```csharp
foreach (var jmeno in studenti)
{
   Console.WriteLine(jmeno);
}
```

Nemá řídící proměnnou (index), takže se nehodí na **naplňování** pole – viz [[05_Pole]].

**Souvisí:** [[01_Operatory_promenne]], [[02_Vstup_vystup]], [[03_Podminky]], [[05_Pole]]
