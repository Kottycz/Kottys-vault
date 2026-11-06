---
aliases: [ref, předávání referencí, předávání odkazem]
tags: [slovnik]
---

# ref

**Klíčové slovo, které předá do metody samotnou proměnnou (ne její kopii) – metoda ji pak může změnit.**

```csharp
static void Swap(ref int x, ref int y)
{
    int temp = x;
    x = y;
    y = temp;
}

int a = 1, b = 2;
Swap(ref a, ref b);   // a = 2, b = 1
```

---

## Podrobně

### Problém, který řeší

Normálně se do metody předá **kopie** hodnoty. Metoda tak změní jen svou kopii, původní proměnná zůstane:

```csharp
static void Pridej(int x) { x = x + 1; }

int a = 5;
Pridej(a);
Console.WriteLine(a);   // pořád 5
```

### S ref

```csharp
static void Pridej(ref int x) { x = x + 1; }

int a = 5;
Pridej(ref a);
Console.WriteLine(a);   // 6
```

Metoda pracuje přímo s **původní proměnnou**, takže změna je vidět venku.

### Pravidla

- `ref` se píše **dvakrát** – v hlavičce metody **i při volání**
- proměnná musí být **před voláním inicializovaná** (mít hodnotu)
- předat jde jen **proměnnou**, ne číslo (`Swap(ref 5, ref 3)` nejde)

### Příklad Swap

Prohození dvou hodnot – klasické použití. Bez `ref` by se prohodily jen kopie uvnitř metody.

### ref a referenční typy

Co je na [[referencni_typ|referenčním typu]] (třeba [[pole]]), se předává jako odkaz i bez `ref` – metoda může **měnit obsah** pole a změna je vidět venku. `ref` je potřeba, až když chceš změnit **samotný odkaz** (nechat proměnnou ukazovat na jiné pole).

### Příbuzné: out

`out` funguje podobně, ale proměnná **nemusí být před voláním inicializovaná** – metoda ji musí naplnit. Používá ho třeba `int.TryParse` – viz [[parse]].

**Souvisí:** [[hodnotovy_typ]], [[referencni_typ]], [[pole]], [[parse]]
