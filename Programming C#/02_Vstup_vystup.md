---
aliases: [Opakování 2, Vstup a výstup]
tags: [opakovani, csharp]
---

# 02 – Vstup a výstup

Opakování k testu. Souvisí s [[konzole]].

## Vstup

Načítá se vždy **[[string|řetězec]]** do proměnné:

```csharp
string zadani = Console.ReadLine();
```

Pokud chceme načíst číslo, musíme převést `string` na číslo – viz [[parse|parsování]]:

```csharp
int cislo = int.Parse(Console.ReadLine());
```

> **Parsování** = převod z textové podoby na nějaký specifický typ, např. číslo.

Načtení znaku z klávesnice (stisk libovolné klávesy) – viz [[readkey|ReadKey]]:

```csharp
Console.ReadKey();
```

## Výstup

| Co | Jak |
| :-- | :-- |
| výpis bez odřádkování | `Console.Write("text");` |
| výpis s odřádkováním | `Console.WriteLine("text");` |
| vynechání řádku | `Console.WriteLine();` nebo `\n` |
| vynechání 2 řádků | `Console.WriteLine("\n");` |

Viz [[write|Write]], [[writeline|WriteLine]] a [[escape_sekvence|escape sekvence]].

## Formátovaný výpis

Tři způsoby, jak vypsat proměnné v textu (viz [[vypis_promennych]]):

```csharp
Console.WriteLine("Součet čísel {0} a {1} je {2}.", cislo1, cislo2, vysledek);

Console.WriteLine("Součet čísel " + cislo1 + " a " + cislo2 + " je " + vysledek + ".");

Console.WriteLine($"Součet čísel {cislo1} a {cislo2} je {vysledek}.");
```

U výpisu probíhá **[[implicitni_konverze|implicitní konverze]]** čísla na `string` – není třeba ho převádět ručně.

**Souvisí:** [[01_Operatory_promenne]], [[03_Podminky]], [[04_Cykly]], [[05_Pole]]
