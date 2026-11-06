---
aliases: [Pole, pole, array, jednorozměrné pole]
tags: [slovnik]
---

# pole

**Datová struktura, která drží víc hodnot stejného typu za sebou; ke každé se přistupuje pomocí indexu.**

```csharp
int[] cisla = new int[5];   // pole pro 5 celých čísel
cisla[0] = 10;              // první prvek
```

---

## Podrobně

### K čemu je

Místo pěti proměnných `a1, a2, a3, a4, a5` máš jedno pole `a` s pěti „přihrádkami". Dá se procházet [[cyklus|cyklem]] a zpracovat naráz.

### Deklarace

```csharp
int[] a;                    // jen deklarace – pole ještě neexistuje (je null)
int[] a = new int[5];       // vytvoření s pamětí pro 5 prvků
int[] a = { 3, 7, 2 };      // rovnou s hodnotami
int[] a = new int[] { 3, 7, 2 };
```

Hranaté závorky `[]` patří za **typ**, ne za jméno: `datovýTyp[] názevPole`.

### Základní vlastnosti

- všechny prvky mají **stejný [[datovy_typ|datový typ]]**
- **velikost je pevná** – po vytvoření ji nejde změnit (na proměnlivou slouží [[kolekce|seznam]])
- prvky jsou očíslované od **0** – viz [[index]]
- počet prvků je ve vlastnosti [[length|Length]]

### Výchozí hodnoty

Nové pole se naplní „nulami" podle typu:

| Typ | Výchozí hodnota |
| :-- | :-- |
| [[int]], [[double]] | `0` |
| [[bool]] | `false` |
| [[char]] | znak s kódem 0 |
| [[string]] a jiné referenční | [[null]] |

### Pole je referenční typ

V proměnné není pole samotné, ale **odkaz** na něj. Přiřazení `b = a` tedy nevytvoří kopii – obě proměnné ukazují na totéž pole. Kopii dělá `Array.Copy` – viz [[array]]. Viz [[referencni_typ]].

### Procházení

```csharp
for (int i = 0; i < a.Length; i++) { Console.WriteLine(a[i]); }   // s indexem
foreach (var x in a) { Console.WriteLine(x); }                    // jen čtení
```

### Další rozměry

Pole může mít víc rozměrů (tabulka) – viz [[dvourozmerne_pole]].

**Souvisí:** [[index]], [[length]], [[array]], [[dvourozmerne_pole]], [[foreach]], [[for]], [[referencni_typ]], [[kolekce]]
