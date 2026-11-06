---
aliases: [Referenční typ, referenční typy, odkazový typ, odkazové typy, reference]
tags: [slovnik]
---

# referenční typ

**Typ, jehož proměnná obsahuje odkaz (referenci) na data uložená jinde v paměti – ne samotná data.**

```csharp
int[] a = { 1, 2, 3 };
int[] b = a;     // b ukazuje na totéž pole
b[0] = 99;       // a[0] je teď také 99
```

---

## Podrobně

### Co sem patří

- [[string]]
- `object`
- [[pole]]
- třídy (včetně vlastních)

### Jak to funguje

Proměnná je jako **lístek s adresou**. Data samotná leží jinde a proměnná říká, kde. Při přiřazení se zkopíruje jen adresa, takže dvě proměnné ukazují na **totéž**.

```
a ──┐
    ├──► [1, 2, 3]
b ──┘
```

### Může být null

Referenční proměnná nemusí ukazovat nikam – pak má speciální hodnotu [[null]], která znamená „žádná data".

```csharp
int[] a = null;       // pole neexistuje
a = new int[5];       // teď existuje
```

### Hodnotový × referenční typ

| | [[hodnotovy_typ\|hodnotový]] | referenční |
| :-- | :-- | :-- |
| V proměnné je | hodnota | odkaz |
| `b = a` | kopie | sdílení stejných dat |
| [[null]] | ne | ano |
| Příklady | [[int]], [[bool]] | [[string]], [[pole]] |

### Předávání do metody

Při předání referenčního typu do metody se předá **odkaz** – metoda může obsah měnit a změna je vidět venku. Na samotný odkaz (zda ukazuje někam jinam) se používá klíčové slovo [[ref]].

### Výjimka: string

[[string]] je referenční typ, ale **nedá se po vytvoření změnit** – každá „úprava" vytvoří nový řetězec. Proto se chová skoro jako hodnotový.

**Souvisí:** [[hodnotovy_typ]], [[null]], [[ref]], [[pole]], [[string]], [[object]]
