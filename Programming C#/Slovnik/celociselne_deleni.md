---
aliases: [Celočíselné dělení]
tags: [slovnik]
---

# celočíselné dělení

**Dělení dvou celých čísel dá zase celé číslo** – desetinná část se zahodí, i když výsledek ukládáš do [[double]].

```csharp
double d = 3 / 4;     // 0  (!!)
double d = 3.0 / 4;   // 0.75
```

---

## Podrobně

### Proč se to děje

C# se o typu výsledku rozhoduje podle **operandů**, ne podle proměnné, kam se výsledek ukládá. Postup u `double d = 3 / 4;`:

1. `3` a `4` jsou oba [[int]]
2. int / int = int → `3 / 4` = **0** (0,75 bez desetinné části)
3. teprve teď se 0 převede na double → `0.0`

Než se výsledek dostane do doublu, desetinná část už je dávno pryč.

### Jak to opravit

Stačí, aby **aspoň jeden** operand byl desetinný:

```csharp
double d = 3.0 / 4;          // 0.75 – desetinná tečka
double d = 3 / 4.0;          // 0.75
double d = (double)a / b;    // 0.75 – přetypování proměnné
double d = 1.0 * a / b;      // 0.75 – trik s násobením
```

### Past s proměnnými

U čísel to je vidět, u proměnných se to snadno přehlédne:

```csharp
int a = 7, b = 2;
double prumer = a / b;           // 3, ne 3.5
double prumer = (double)a / b;   // 3.5
```

### Past v Math.Pow

```csharp
Math.Pow(1000, 1 / 3);     // 1   – 1/3 = 0, x⁰ = 1
Math.Pow(1000, 1.0 / 3);   // 10
```

### Kdy se hodí

Někdy je to přesně to, co chceš – třeba počet celých hodin:

```csharp
int minuty = 135;
int hodiny = minuty / 60;    // 2
int zbytek = minuty % 60;    // 15
```

Zbytek po dělení vrací `%` – viz [[aritmeticke_operatory|aritmetické operátory]].

**Souvisí:** [[int]], [[double]], [[aritmeticke_operatory]], [[pretypovani]], [[math]]
