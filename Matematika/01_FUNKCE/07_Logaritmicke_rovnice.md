---
aliases: [Logaritmické rovnice]
tags: [matematika, rovnice]
---

# Logaritmické rovnice

Rovnice, kde je **neznámá v argumentu logaritmu**.

## Vždy nejdřív podmínky

- **argument každého logaritmu $> 0$**
- (základ $> 0$ a $\neq 1$, pokud obsahuje neznámou)
- řeším jen v průniku podmínek, nakonec **zkouška / kontrola podmínek**

## Typy a postupy

1. **$\log_a f(x) = c$** → odlogaritmování: $f(x) = a^c$
2. **$\log_a f(x) = \log_a g(x)$** → $f(x) = g(x)$ (log. funkce je prostá)
3. **součty, rozdíly, násobky** → pomocí vět ([[06_Logaritmicka_funkce]]) sjednotit na **jeden logaritmus** na každé straně, pak jako 1. nebo 2.
4. **mocniny logaritmů** ($\log^2 x$ ...) → [[substituce]] $t = \log_a x$, vyřešit pro $t$ a vrátit se k $x$

Číslo jako logaritmus: $2 = \log_a a^2$, např. $3 = \log 1000$.

---

## Vypočtené příklady

### 1) Základní tvar

$\log_2 x = 3$

Podmínka: $x > 0$. $x = 2^3$

$x = 8$

### 2) S výrazem v argumentu

$\log_3 (2x + 1) = 2$

1. podmínka: $2x + 1 > 0 \Rightarrow x > -\tfrac12$
2. odlogaritmuju: $2x + 1 = 3^2 = 9$
3. $2x = 8$

$x = 4$ (splňuje podmínku ✓)

### 3) Logaritmus = logaritmus

$\log_2 (x^2 + x) = \log_2 (-2x)$

1. podmínky: $x^2 + x > 0$ ($x < -1$ nebo $x > 0$) a $-2x > 0$ ($x < 0$) → $x < -1$
2. $x^2 + x = -2x \Rightarrow x^2 + 3x = 0 \Rightarrow x(x + 3) = 0$
3. $x = 0$ nebo $x = -3$
4. $x = 0$ podmínku **nesplňuje**

$x = -3$

Zkouška: $\log_2 (9 - 3) = \log_2 6$ a $\log_2 (6) = \log_2 6$ ✓

### 4) Součet logaritmů

$\log_2 x + \log_2 (x - 1) = 1$

1. podmínky: $x > 0$ a $x > 1$ → $x > 1$
2. $\log_2 [x(x-1)] = 1 \Rightarrow x(x-1) = 2$
3. $x^2 - x - 2 = 0 \Rightarrow (x - 2)(x + 1) = 0$
4. $x = 2$ nebo $x = -1$ (**$-1$ nevyhovuje podmínce**)

$x = 2$

### 5) Součet s neznámou, kvadratika

$\log_6 (x + 16) + \log_6 x = 1$

1. podmínky: $x > -16$ a $x > 0$ → $x > 0$
2. $\log_6 [x(x+16)] = 1 \Rightarrow x(x + 16) = 6$
3. $x^2 + 16x - 6 = 0$, $D = 256 + 24 = 280$, $x = \dfrac{-16 \pm 2\sqrt{70}}{2} = -8 \pm \sqrt{70}$
4. $-8 + \sqrt{70} \doteq 0{,}367 > 0$ ✓, $-8 - \sqrt{70} < 0$ ✗

$x = -8 + \sqrt{70}$

### 6) Substituce

$\log^2 x - \log x - 2 = 0$

1. podmínka $x > 0$, substituce $t = \log x$
2. $t^2 - t - 2 = 0 \Rightarrow (t - 2)(t + 1) = 0 \Rightarrow t = 2$ nebo $t = -1$
3. $\log x = 2 \Rightarrow x = 100$; $\log x = -1 \Rightarrow x = 0{,}1$

$x \in \{0{,}1;\, 100\}$ (obě $> 0$ ✓)

---

**Souvisí:** [[05_Exponencialni_rovnice]], [[06_Logaritmicka_funkce]], [[Matematika]]
