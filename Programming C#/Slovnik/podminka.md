---
aliases: [Podmínka, if, else, else if, větvení]
tags: [slovnik]
---

# podmínka

**Příkaz `if` provede blok kódu jen tehdy, když je zadaný výraz pravdivý (`true`).**

```csharp
if (a > 5)
{
    Console.WriteLine("a je větší než 5");
}
```

---

## Podrobně

### Jak funguje

V závorce za `if` je výraz, jehož výsledek je [[bool]]. Když je `true`, provede se blok ve složených závorkách. Když je `false`, blok se přeskočí a program pokračuje za ním.

### Varianty

| Zápis | Význam |
| :-- | :-- |
| `if` | provede blok, když podmínka platí |
| `if … else` | když platí, provede první blok, **jinak** druhý |
| `if … else if … else` | postupně zkouší víc podmínek |

```csharp
if (znamka == 1)
{
    Console.WriteLine("výborný");
}
else if (znamka == 2)
{
    Console.WriteLine("chvalitebný");
}
else
{
    Console.WriteLine("jiná známka");
}
```

### Pořadí vyhodnocení

Podmínky se kontrolují **shora dolů** a provede se jen **první**, která platí. Zbytek se přeskočí, i kdyby také platil. `else` na konci zachytí všechno ostatní.

### Co může být v podmínce

- porovnání – [[relacni_operatory|relační operátory]] (`==`, `!=`, `>`, `<`, `>=`, `<=`)
- spojení více podmínek – [[logicke_operatory|logické operátory]] (`&&`, `||`, `!`)
- proměnná typu [[bool]] přímo: `if (jeSude)`

### Pozor na `=` a `==`

`=` je [[prirazeni|přiřazení]], `==` je porovnání. V C# `if (a = 5)` **nejde přeložit** (číslo není bool), takže se chyba odhalí hned – v jazyce C by se tiše provedlo přiřazení.

### Složené závorky

U jednoho příkazu jdou vynechat, ale **doporučuje se je psát vždy** – při pozdějším přidání dalšího řádku se pak nic nerozbije.

### Zkrácený zápis

Na jednoduchý výběr mezi dvěma hodnotami slouží [[ternarni_operator|ternární operátor]]:

```csharp
string stav = vek >= 18 ? "dospělý" : "nezletilý";
```

### Když je větví hodně

Při porovnávání jedné hodnoty s mnoha možnostmi je přehlednější [[switch]].

**Souvisí:** [[switch]], [[bool]], [[relacni_operatory]], [[logicke_operatory]], [[ternarni_operator]], [[cyklus]]
