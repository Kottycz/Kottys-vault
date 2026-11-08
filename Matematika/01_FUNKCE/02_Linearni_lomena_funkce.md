---
aliases: [Lineární lomená funkce, Hyperbola, Nepřímá úměrnost]
tags: [matematika, funkce]
---

# Lineární lomená funkce

Obecný tvar: $y = \dfrac{ax + b}{cx + d}$, kde $c \neq 0$ a $ad - bc \neq 0$.

Grafem je [[hyperbola (funkce)|hyperbola]]. Základ je **nepřímá úměrnost** $y = \dfrac{k}{x}$.

## Nepřímá úměrnost $y = k/x$

- $D(f) = \mathbb{R} \setminus \{0\}$, $H(f) = \mathbb{R} \setminus \{0\}$
- **lichá** funkce (souměrná podle počátku)
- [[asymptota|asymptoty]]: osy $x = 0$ a $y = 0$
- **k > 0** – větve v 1. a 3. kvadrantu, na každém intervalu **klesající**
- **k < 0** – větve ve 2. a 4. kvadrantu, na každém intervalu **rostoucí**
- větší $|k|$ = větve dál od středu

## Základní (posunutý) tvar

$$y = \frac{k}{x - a} + b$$

| co | hodnota |
|---|---|
| střed hyperboly | $S[a;\, b]$ |
| svislá asymptota | $x = a$ |
| vodorovná asymptota | $y = b$ |
| $D(f)$ | $\mathbb{R} \setminus \{a\}$ |
| $H(f)$ | $\mathbb{R} \setminus \{b\}$ |

**Pozor na znaménka:** $x + 2$ znamená $a = -2$ (posun doleva), $-2$ na konci znamená $b = -2$ (posun dolů).

## Úprava předpisu na základní tvar

Zlomek, kde je $x$ i v čitateli, rozložím tak, aby $x$ zůstalo jen ve jmenovateli:

1. v čitateli udělám **násobek jmenovatele** + zbytek
2. rozdělím zlomek
3. nebo **dělím mnohočleny**: $(2x + 3) : (x + 1) = 2$, zbytek $1$

## Kreslení grafu

1. úprava na tvar $\dfrac{k}{x-a} + b$
2. nakreslím **asymptoty** (čárkovaně) a střed
3. načrtnu $y = k/x$ s počátkem ve středu $S$
4. pro přesnost spočítám průsečíky s osami

---

## Vypočtené příklady

### 1) Graf z nepřímé úměrnosti

$y = \dfrac{1}{x} + 1$

- posun $y = 1/x$ o **1 nahoru**
- střed $[0;\, 1]$, asymptoty $x = 0$, $y = 1$
- $D(f) = \mathbb{R} \setminus \{0\}$, $H(f) = \mathbb{R} \setminus \{1\}$

### 2) Vlastnosti a průsečíky

$y = \dfrac{1}{x+1} - 2$

- $a = -1$, $b = -2$ → střed $S[-1;\, -2]$
- $D(f) = \mathbb{R} \setminus \{-1\}$, $H(f) = \mathbb{R} \setminus \{-2\}$
- osa y ($x = 0$): $y = 1 - 2 = -1$ → $[0;\, -1]$
- osa x ($y = 0$): $\dfrac{1}{x+1} = 2 \Rightarrow x + 1 = \tfrac12 \Rightarrow x = -\tfrac12$ → $[-\tfrac12;\, 0]$
- $k = 1 > 0$ → na obou intervalech klesající

### 3) Úprava předpisu (vytýkání)

$y = \dfrac{x+3}{x+1}$

$$y = \frac{(x+1) + 2}{x+1} = 1 + \frac{2}{x+1}$$

$k = 2$, střed $S[-1;\, 1]$

### 4) Úprava předpisu

$y = \dfrac{2x+3}{x+1}$

Čitatel: $2x + 3 = 2(x+1) + 1$

$$y = \frac{2(x+1) + 1}{x+1} = 2 + \frac{1}{x+1}$$

Střed $S[-1;\, 2]$, $D(f) = \mathbb{R} \setminus \{-1\}$, $H(f) = \mathbb{R} \setminus \{2\}$.

### 5) Úprava předpisu

$y = \dfrac{3x-5}{x-2}$

Čitatel: $3x - 5 = 3(x-2) + 1$

$$y = 3 + \frac{1}{x-2}$$

Střed $S[2;\, 3]$.

### 6) Úprava, když má $x$ ve jmenovateli koeficient

$y = \dfrac{3x+1}{2x-4}$

1. jmenovatel: $2x - 4 = 2(x-2)$
2. čitatel: $3x + 1 = 3(x-2) + 7$

$$y = \frac{3(x-2) + 7}{2(x-2)} = \frac{3}{2} + \frac{7}{2(x-2)}$$

$k = \tfrac72$, střed $S[2;\, \tfrac32]$.

### 7) Hledání předpisu

Najdi lineární lomenou funkci s $D(f) = \mathbb{R} \setminus \{2\}$, $H(f) = \mathbb{R} \setminus \{-1\}$, graf prochází $[3;\, -3]$.

1. z $D$ a $H$: $a = 2$, $b = -1$ → $y = \dfrac{k}{x-2} - 1$
2. dosadím bod: $-3 = \dfrac{k}{3-2} - 1 \Rightarrow k = -2$

$$y = \frac{-2}{x-2} - 1$$

---

**Souvisí:** [[01_Vlastnosti_funkci]], [[03_Mocninna_funkce]], [[Matematika]]
