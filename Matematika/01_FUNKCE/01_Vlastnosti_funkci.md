---
aliases: [Vlastnosti funkcí, Funkce, Definiční obor, Kvadratická funkce, Lineární funkce]
tags: [matematika, funkce]
---

# Vlastnosti funkcí

**[[funkce]]** přiřazuje každému prvku z [[definiční obor|definičního oboru]] $D(f)$ **právě jedno** číslo z [[obor hodnot|oboru hodnot]] $H(f)$.

- $D(f)$ = čísla na ose **x**, která můžu dosadit
- $H(f)$ = čísla na ose **y**, která mi můžou vyjít
- zadání: **předpisem**, **tabulkou**, **grafem**
- **test svislou přímkou** – graf funkce nesmí mít dva body nad sebou

## Definiční obor (pravidla)

Z $\mathbb{R}$ vyhodím všechno, co nejde spočítat:

- **jmenovatel** $\neq 0$
- pod **odmocninou** (sudou) výraz $\geq 0$
- v **logaritmu** výraz $> 0$

## Sudá / lichá

- [[sudá funkce]]: $f(-x) = f(x)$, graf souměrný podle osy **y**
- [[lichá funkce]]: $f(-x) = -f(x)$, graf souměrný podle počátku
- aby to šlo určit, musí být $D(f)$ souměrný podle nuly

## Monotonie, omezenost, extrémy

- **rostoucí**: $x_1 < x_2 \Rightarrow f(x_1) < f(x_2)$
- **klesající**: $x_1 < x_2 \Rightarrow f(x_1) > f(x_2)$
- viz [[monotonie]]
- **omezená** – grafem nepřekročí vodorovnou hranici (shora / zdola)
- **maximum / minimum** – největší / nejmenší hodnota funkce
- **prostá** funkce – každé $y$ vzniklo z jediného $x$ ([[prostá funkce]])

## Lineární funkce

$y = kx + q$

- $k$ = směrnice (**k > 0** rostoucí, **k < 0** klesající, **k = 0** konstantní)
- $q$ = průsečík s osou y
- $D = H = \mathbb{R}$ (pro $k \neq 0$)

## Kvadratická funkce

$y = ax^2 + bx + c$, graf je **parabola** ([[kvadratická funkce]])

- **a > 0** – otevřená nahoru, má **minimum**
- **a < 0** – otevřená dolů, má **maximum**
- doplnění na čtverec: $y = a(x - m)^2 + n$ → **vrchol** $V[m; n]$
- osa paraboly: $x = m$

## Grafické řešení rovnic a nerovnic

- $f(x) = g(x)$ → x-ové souřadnice **průsečíků** grafů
- $f(x) > g(x)$ → tam, kde je graf $f$ **nad** grafem $g$

---

## Vypočtené příklady

### 1) Definiční obor

$f(x) = \dfrac{\sqrt{x+2}}{x-3}$

- odmocnina: $x + 2 \geq 0 \Rightarrow x \geq -2$
- jmenovatel: $x - 3 \neq 0 \Rightarrow x \neq 3$

$D(f) = \langle -2;\, 3) \cup (3;\, \infty)$

### 2) Definiční obor a obor hodnot

$y = \dfrac{1}{2x-1} + 2$

- $2x - 1 \neq 0 \Rightarrow x \neq \tfrac12$ → $D(f) = \mathbb{R} \setminus \{\tfrac12\}$
- zlomek $\dfrac{1}{2x-1}$ **nikdy nebude 0**, takže celý výraz nikdy nebude 2 → $H(f) = \mathbb{R} \setminus \{2\}$

### 3) Sudá, lichá, ani jedna

- $f(x) = x^3 - x$: $f(-x) = -x^3 + x = -(x^3 - x) = -f(x)$ → **lichá**
- $g(x) = x^2 + 1$: $g(-x) = x^2 + 1 = g(x)$ → **sudá**
- $h(x) = x^2 + x$: $h(-x) = x^2 - x$, což není $h(x)$ ani $-h(x)$ → **ani sudá, ani lichá**

### 4) Je to funkce?

| x | 1 | 2 | 3 | 3 |
|---|---|---|---|---|
| y | 1 | 2 | 3 | 2 |

Číslu $3$ jsou přiřazena dvě různá $y$ → **není funkce** (v grafu by byly dva body nad sebou).

### 5) Přímka ze dvou bodů

Přímka prochází $A[1;\,3]$ a $B[3;\,7]$.

1. $k = \dfrac{7-3}{3-1} = 2$
2. dosadím $A$: $3 = 2\cdot 1 + q \Rightarrow q = 1$

$y = 2x + 1$

Průsečík s osou x: $0 = 2x + 1 \Rightarrow x = -\tfrac12$, tedy $[-\tfrac12;\, 0]$.

### 6) Kvadratická funkce

$y = x^2 - 4x + 1$

1. doplním na čtverec: $y = (x-2)^2 - 4 + 1 = (x-2)^2 - 3$
2. vrchol $V[2;\, -3]$, $a = 1 > 0$ → minimum $-3$
3. $H(f) = \langle -3;\, \infty)$
4. klesající na $(-\infty;\, 2\rangle$, rostoucí na $\langle 2;\, \infty)$
5. průsečík s osou y: $[0;\, 1]$
6. průsečíky s osou x: $(x-2)^2 = 3 \Rightarrow x = 2 \pm \sqrt{3}$

### 7) Kvadratická nerovnice

$x^2 - 4x + 1 \geq -2$

$(x-2)^2 - 3 \geq -2 \Rightarrow (x-2)^2 \geq 1 \Rightarrow |x-2| \geq 1$

$x \leq 1$ nebo $x \geq 3$ → $x \in (-\infty;\, 1\rangle \cup \langle 3;\, \infty)$

Graficky: parabola leží nad (nebo na) přímkou $y = -2$ mimo interval $(1;\, 3)$.

---

**Souvisí:** [[02_Linearni_lomena_funkce]], [[03_Mocninna_funkce]], [[Matematika]]
