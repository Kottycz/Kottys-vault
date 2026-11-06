---
aliases: [switch, case, default]
tags: [slovnik]
---

# switch

**Větvení, které porovná jednu hodnotu s několika možnostmi (`case`) a provede tu, která se shoduje.**

```csharp
switch (den)
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

---

## Podrobně

### Části

| Část | Význam |
| :-- | :-- |
| `switch (výraz)` | hodnota, která se testuje |
| `case hodnota:` | větev, která se provede, když se výraz **rovná** hodnotě |
| `break;` | ukončí větev – program skočí za celý switch |
| `default:` | provede se, když nesedí **žádný** case (obdoba `else`) |

### Break je povinný

V C# musí každá větev s kódem skončit příkazem `break` (nebo `return`). Program **nepropadá** do další větve jako v jazycích C nebo Java. Zapomenutý `break` je chyba při překladu.

### Více hodnot na jednu větev

Prázdné `case` pod sebou se spojí:

```csharp
switch (den)
{
    case 6:
    case 7:
        Console.WriteLine("víkend");
        break;
    default:
        Console.WriteLine("pracovní den");
        break;
}
```

### Testovaný výraz (to v závorce)

V závorce za `switch` je **testovaný výraz**. Je to to, co switch zkoumá – nejčastěji **proměnná**, ve které je uložena nějaká hodnota.

Program se podívá, **jakou hodnotu ta proměnná právě má** (např. `den` je `2`), a pak ji porovnává s hodnotami u jednotlivých `case`. Jakmile najde `case` se stejnou hodnotou, provede kód, který je pod ním.

Pro `switch (den)` když `den = 2`:

- `case 1` → `2` se nerovná `1`, přeskočí se
- `case 2` → `2` se rovná `2`, **provede se**

**Jak to funguje, krok za krokem** (pro `switch (den)` s `den = 2` z příkladu nahoře):

1. výraz v závorce se **vyhodnotí jednou**, hned na začátku (`den` → `2`)
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

### Co se dá testovat

Testovaný výraz má **datový typ** – takový, jaký má to, co je v závorce. Je-li v závorce proměnná typu `string`, je celý výraz typu `string`. Je-li tam `char`, je typu `char`.

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

Celá čísla ([[int]]), [[char]], [[string]] a výčtové typy. Hodnoty u `case` musí být **konstanty** (číslo, znak, text nebo [[konstanta]]):

- proměnná tam nejde
- každá hodnota může být jen **jednou** – dvě stejné `case` jsou chyba
- rozsah (`case > 5`) tam nejde

### switch vs. if

| | [[podminka\|if]] | switch |
| :-- | :-- | :-- |
| Porovnání | libovolné, i rozsahy (`vek >= 18`) | jen **shoda** s konkrétní hodnotou |
| Kdy se hodí | málo větví, složité podmínky | hodně hodnot jedné proměnné (dny, menu, volba 1–5) |

### Typické použití

Menu v konzolové aplikaci:

```csharp
string volba = Console.ReadLine();
switch (volba)
{
    case "a": /* … */ break;
    case "b": /* … */ break;
    default: Console.WriteLine("neplatná volba"); break;
}
```

**Souvisí:** [[podminka]], [[break]], [[int]], [[string]], [[char]]
