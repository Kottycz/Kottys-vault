---
aliases: [decimal]
tags: [slovnik]
---

# decimal

**[[hodnotovy_typ|Hodnotový typ]] pro desetinná čísla s velmi vysokou přesností a menším rozsahem – hodí se na peníze.**

```csharp
decimal cena = 199.90m;   // za číslem musí být m
```

---

## Podrobně

### Vlastnosti

| | [[float]] | [[double]] | decimal |
| :-- | :-- | :-- | :-- |
| Velikost | 32 bitů | 64 bitů | **128 bitů** |
| Platné číslice | ~7 | ~15 | **~28** |
| Rozsah | největší | velký | **nejmenší** (cca ±7,9 · 10²⁸) |
| Přípona | `f` | – | **`m`** |

V učivu: **speciální typ – větší přesnost, menší rozsah.**

### Proč na peníze

[[float]] i [[double]] ukládají čísla ve **dvojkové soustavě**, kde se některá desetinná čísla (třeba 0,1) nedají zapsat přesně. Při počítání se hromadí drobné chyby:

```csharp
double d = 0.1 + 0.2;     // 0.30000000000000004
decimal m = 0.1m + 0.2m;  // 0.3 přesně
```

`decimal` počítá v **desítkové soustavě**, takže u peněz žádné chyby nevznikají.

### Přípona m

Desetinné číslo v kódu je ve výchozím stavu [[double]]. Aby bylo `decimal`, musí za ním být `m`:

```csharp
decimal a = 5.5;    // CHYBA – double nejde do decimalu samo
decimal a = 5.5m;   // OK
```

### Nevýhody

- **pomalejší** než double
- zabírá **víc paměti**
- nemá tak velký rozsah
- funkce z [[math|Math]] jsou pro double (u decimalu jich je méně)

### Kdy ho použít

Finance, účetnictví, ceny, daně. Na fyziku a vědecké výpočty stačí [[double]].

**Souvisí:** [[double]], [[float]], [[datovy_typ]], [[hodnotovy_typ]], [[math]]
