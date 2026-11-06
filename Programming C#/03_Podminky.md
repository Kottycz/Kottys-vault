---
aliases: [Opakování 3, Podmínky, Větvení]
tags: [opakovani, csharp]
---

# 03 – Podmínky a větvení

Opakování k testu. Výsledek [[podminka|podmínky]] je vždy [[bool]].

## Operátory v podmínce

| [[relacni_operatory\|Relační]] | Význam |
| :-- | :-- |
| `==` | rovná se |
| `!=` | nerovná se |
| `>` `<` | větší, menší |
| `>=` `<=` | větší/menší nebo rovno |

**Logické spojky** (viz [[logicke_operatory]]): `!` negace, `&&` and, `||` or

## if

```csharp
if (podmínka)
{
   blok příkazů
}
```

## if else

```csharp
if (podmínka)
{
   blok příkazů
}
else
{
   blok příkazů
}
```

## if else if

```csharp
if (podmínka)
{
   blok příkazů
}
else if (podmínka)
{
   blok příkazů
}
...
else
{
   blok příkazů
}
```

Podmínky se vyhodnocují **shora dolů** – provede se první, která platí. `else` na konci zachytí všechno ostatní.

## switch

Viz [[switch]].

```csharp
switch (testovaný výraz)
{
   case hodnota1:
      // provede se, když výraz nabývá hodnotu hodnota1
      break;
   case hodnota2:
      // provede se, když výraz nabývá hodnotu hodnota2
      break;
   ...
   default:
      // provede se, když výraz nenabývá žádnou z předchozích hodnot
      break;
}
```

- `break` ukončí větev – viz [[break]] – bez něj kód neprojde (v C# je povinný)
- `default` je obdoba `else`

### Testovaný výraz (to v závorce)

V závorce za `switch` je **testovaný výraz**. Je to to, co switch zkoumá – nejčastěji **proměnná**, ve které je uložena nějaká hodnota.

Program se podívá, **jakou hodnotu ta proměnná právě má** (např. `den` je `2`), a pak ji porovnává s hodnotami u jednotlivých `case`. Jakmile najde `case` se stejnou hodnotou, provede kód, který je pod ním.

Pro `switch (den)` když `den = 2`:

- `case 1` → `2` se nerovná `1`, přeskočí se
- `case 2` → `2` se rovná `2`, **provede se**

```csharp
int den = 2;

switch (den)          // testovaný výraz = den
{
   case 1:
      Console.WriteLine("pondělí");
      break;
   case 2:
      Console.WriteLine("úterý");
      break;
   default:
      Console.WriteLine("jiný den");
      break;
}
```

**Jak to funguje, krok za krokem:**

1. výraz v závorce se **vyhodnotí jednou**, hned na začátku (tady `den` → `2`)
2. ta hodnota se porovnává s hodnotami u `case` **shora dolů**: `1`? ne. `2`? ano.
3. provede se **první větev, kde se hodnota shoduje** (`case 2`) → vypíše se "úterý"
4. `break` ukončí celý switch, zbylé větve se už neprohledávají
5. kdyby se nic neshodovalo (třeba `den = 5`), provede se `default`
6. kdyby se nic neshodovalo a `default` by chyběl, **neprovede se nic**

**Co se stane pro různé hodnoty `den`:**

| `den` | Co se provede | Výpis |
| :-- | :-- | :-- |
| `1` | `case 1` | pondělí |
| `2` | `case 2` | úterý |
| `5` | `default` | jiný den |

**Co může být testovaný výraz:**

| Co | Příklad | Poznámka |
| :-- | :-- | :-- |
| proměnná | `switch (den)` | nejčastější |
| výpočet | `switch (cislo % 2)` | nejdřív se spočítá, pak se výsledek porovnává (zbytek po dělení 2 je `0` nebo `1`) |
| volání metody | `switch (Console.ReadLine())` | metoda se zavolá **jednou** a výsledek se použije |

**Proto se vyhodnocuje jen jednou:** u `switch (Console.ReadLine())` se program zeptá uživatele jednou. Kdyby se výraz přepočítával u každého `case`, čekal by na vstup znovu a znovu.

**Jakého typu je testovaný výraz:**

Testovaný výraz má **datový typ** – takový, jaký má to, co je v závorce. Je-li v závorce proměnná typu `string`, je celý výraz typu `string`. Je-li tam `char`, je typu `char`. A tak dál.

**Hodnoty u `case` musí být stejného typu jako výraz**, protože se porovnávají. Nemůžeš porovnat číslo s textem.

```csharp
int cislo = 2;
switch (cislo)            // výraz je typu int
{
   case 1:  break;        // case je číslo → OK
   case 2:  break;
}
```

```csharp
char znak = 'a';
switch (znak)             // výraz je typu char
{
   case 'a':  break;      // case je znak v jednoduchých uvozovkách → OK
   case 'b':  break;
}
```

```csharp
string slovo = "ano";
switch (slovo)            // výraz je typu string
{
   case "ano":  break;    // case je text v dvojitých uvozovkách → OK
   case "ne":   break;
}
```

| Typ výrazu | `case` musí být | Uvozovky |
| :-- | :-- | :-- |
| [[int]] | číslo – `case 1:` | žádné |
| [[char]] | jeden znak – `case 'a':` | **jednoduché** `' '` |
| [[string]] | text – `case "ano":` | **dvojité** `" "` |

Když typy nesedí, program se **nepřeloží** (chyba):

```csharp
int cislo = 2;
switch (cislo)
{
   case "ano":  break;    // CHYBA – výraz je int, case je text
}
```

**Pravidla pro `case`:**

- hodnota musí být **konstanta** (číslo, znak, text nebo [[konstanta]]) – proměnná tam nejde
- každá hodnota může být jen **jednou** – dvě stejné `case` jsou chyba
- rozsah (`case > 5`) tam nejde

**Pozor:** `switch` porovnává jen **shodu** (`==`). Na "větší než" nebo "od – do" použij [[podminka|if]].

### if vs. switch

| | `if` | `switch` |
| :-- | :-- | :-- |
| Podmínka | libovolná (i rozsahy) | porovnání jedné hodnoty |
| Kdy použít | `vek >= 18` | `den == 1, 2, 3…` |

## Zkrácený zápis

Jednoduchou podmínku jde zapsat [[ternarni_operator|ternárním operátorem]]:

```csharp
b = a > 5 ? 1 : 2;
```

**Souvisí:** [[01_Operatory_promenne]], [[02_Vstup_vystup]], [[04_Cykly]], [[05_Pole]]
