---
aliases: [Opakování 5, Pole]
tags: [opakovani, csharp]
---

# 05 – Pole

Opakování k testu. Pole je **[[referencni_typ|referenční typ]]** – viz [[01_Operatory_promenne]]. Podrobně: [[pole]].

## Co to je

**Datová struktura, která obsahuje více položek stejného [[datovy_typ|datového typu]] za sebou.** K jednotlivým položkám se přistupuje pomocí **[[index|indexu]]** – celočíselné proměnné.

## Deklarace

```csharp
datovýTyp[] názevPole;                                 // jen deklarace
datovýTyp[] názevPole = new datovýTyp[početPrvků];     // s pamětí pro prvky
```

Příklad:

```csharp
int[] cisla = new int[5];   // pole pro 5 celých čísel
cisla[0] = 10;              // indexuje se od 0
```

## Length

Pole má vlastnost **[[length|`Length`]]**, kde je uložena jeho délka (počet prvků):

```csharp
for (int i = 0; i < cisla.Length; i++)
{
   Console.WriteLine(cisla[i]);
}
```

## foreach

Zjednodušená verze cyklu pro práci s kolekcemi – projde všechny prvky v poli a **jeho délku si zjistí sám** (viz [[04_Cykly]]):

```csharp
foreach (datovytyp promenna in kolekce)
{
    // příkazy
}
```

`foreach` **nemá řídící proměnnou**, proto není vhodný pro naplňování pole – jen pro jeho procházení.

## Metody třídy [[array|Array]]

| Metoda | Co dělá |
| :-- | :-- |
| `Array.Sort(nazevPole)` | setřídí pole |
| `Array.Reverse(nazevPole)` | obrátí pořadí prvků (pole pozpátku) |
| `Array.Copy(puvodniPole, novePole, pocetPrvku)` | zkopíruje jedno pole do druhého se zadaným počtem prvků |

## Dvourozměrné pole

Podrobně: [[dvourozmerne_pole]].

```csharp
datovýTyp[,] názevPole = new datovýTyp[počet1, počet2];
```

- `Length` vrátí **celkový počet prvků** (řádky × sloupce)
- `GetLength()` vrátí počet prvků v řádcích a sloupcích – parametr `0` (řádky) a `1` (sloupce)

```csharp
int[,] matice = new int[3, 4];
matice.Length;        // 12
matice.GetLength(0);  // 3
matice.GetLength(1);  // 4
```

**Souvisí:** [[01_Operatory_promenne]], [[02_Vstup_vystup]], [[03_Podminky]], [[04_Cykly]]
