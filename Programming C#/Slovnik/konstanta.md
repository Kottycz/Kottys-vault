---
aliases: [Konstanta, const]
tags: [slovnik]
---

# konstanta

**Hodnota, kterou po deklaraci nejde změnit.** Klíčové slovo `const`.

```csharp
const int g = 5;
```

---

## Podrobně

### Pravidla

- hodnota se musí zadat **hned při deklaraci**
- hodnota musí být známá už při kompilaci – nejde do ní uložit třeba vstup od uživatele
- pokus o změnu je chyba kompilace

```csharp
const int g = 5;
g = 6;                                        // CHYBA
const int x = int.Parse(Console.ReadLine());  // CHYBA – není známé předem
```

### K čemu je

- **Čitelnost** – `POCET_DNI_V_TYDNU` řekne víc než `7` uprostřed kódu
- **Jedna změna na jednom místě** – když se hodnota změní (třeba sazba DPH), přepíše se jen na jednom řádku
- **Ochrana před chybou** – nejde ji omylem přepsat

```csharp
const double DPH = 0.21;
double cenaSDph = cena * (1 + DPH);
```

### Konstanty z Math

Třída [[math|Math]] má vlastní konstanty:

- `Math.PI` – 3,14159…
- `Math.E` – 2,71828… (Eulerovo číslo)

```csharp
double obsahKruhu = Math.PI * r * r;
```

**Souvisí:** [[promenna]], [[datovy_typ]], [[math]]
