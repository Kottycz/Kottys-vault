---
aliases: [do while, do-while, cyklus do while]
tags: [slovnik]
---

# do while

**[[cyklus|Cyklus]] s podmínkou na konci – tělo proběhne vždy aspoň jednou a pak se opakuje, dokud podmínka platí.**

```csharp
int cislo;
do
{
    Console.Write("Zadej kladné číslo: ");
    cislo = int.Parse(Console.ReadLine());
}
while (cislo <= 0);
```

---

## Podrobně

### Zápis

```csharp
do
{
    tělo cyklu
}
while (podmínka);
```

Za `while (podmínka)` se píše **středník** – u obyčejného [[while]] ne.

### Rozdíl oproti while

| | [[while]] | do while |
| :-- | :-- | :-- |
| Podmínka | před tělem | **po** těle |
| Minimální počet průchodů | 0 | **1** |

### Kdy se hodí

Když potřebuješ **nejdřív něco udělat a až pak zjistit, jestli opakovat**. Klasický případ je kontrola vstupu: uživatele musíš nejdřív požádat o číslo, teprve potom můžeš zkontrolovat, jestli je správné.

```csharp
string heslo;
do
{
    Console.Write("Heslo: ");
    heslo = Console.ReadLine();
}
while (heslo != "tajne");
```

### Pozor

Proměnná použitá v podmínce musí být deklarovaná **před** cyklem (jako `cislo` v příkladu nahoře) – uvnitř bloku `{ }` by ji podmínka za ním neviděla.

### Srovnání všech cyklů

| Cyklus | Podmínka | Použití |
| :-- | :-- | :-- |
| [[for]] | na začátku | známý počet |
| [[while]] | na začátku | neznámý počet, může proběhnout 0× |
| **do while** | na konci | neznámý počet, aspoň 1× |

**Souvisí:** [[cyklus]], [[while]], [[for]], [[podminka]], [[readline]]
