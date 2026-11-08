---
aliases: [Mocninná funkce, Inverzní funkce, Mocninné funkce]
tags: [matematika, funkce]
---

# Mocninná funkce a inverzní funkce

Tvar: $y = x^n$, kde $n \in \mathbb{Z}$ (celé číslo).

## $n$ přirozené (kladné)

| | **n sudé** ($x^2, x^4, \dots$) | **n liché** ($x, x^3, x^5, \dots$) |
|---|---|---|
| $D(f)$ | $\mathbb{R}$ | $\mathbb{R}$ |
| $H(f)$ | $\langle 0;\, \infty)$ | $\mathbb{R}$ |
| parita | [[sudá funkce]] | [[lichá funkce]] |
| monotonie | klesající na $(-\infty; 0\rangle$, rostoucí na $\langle 0; \infty)$ | rostoucí |
| omezenost | zdola (min. 0) | neomezená |

Všechny procházejí body $[0;0]$ a $[1;1]$.

## $n$ celé záporné

$y = x^{-n} = \dfrac{1}{x^n}$, $D(f) = \mathbb{R} \setminus \{0\}$

| | **n sudé** ($x^{-2}, x^{-4}, \dots$) | **n liché** ($x^{-1}, x^{-3}, \dots$) |
|---|---|---|
| $H(f)$ | $(0;\, \infty)$ | $\mathbb{R} \setminus \{0\}$ |
| parita | sudá | lichá |
| monotonie | rostoucí na $(-\infty; 0)$, klesající na $(0; \infty)$ | klesající na $(-\infty; 0)$ i na $(0; \infty)$ |
| [[asymptota|asymptoty]] | $x = 0$, $y = 0$ | $x = 0$, $y = 0$ |

## Porovnávání mocnin

- na $(0;\, 1)$: vyšší mocnina = **menší** hodnota ($x^5 < x^2$)
- na $(1;\, \infty)$: vyšší mocnina = **větší** hodnota ($x^5 > x^2$)
- v bodech $0$, $1$ (a $-1$) se grafy protínají
- graf $x^{n+1}$ vznikne z grafu $x^n$ **vynásobením hodnotou x** (grafické násobení)

## Inverzní funkce

[[inverzní funkce]] $f^{-1}$ „vrací zpátky“: pokud $f(a) = b$, pak $f^{-1}(b) = a$.

- existuje jen k **[[prostá funkce|prosté]]** funkci
- $D(f^{-1}) = H(f)$ a $H(f^{-1}) = D(f)$
- graf $f^{-1}$ je souměrný s grafem $f$ podle přímky $y = x$
- **sudá funkce** inverzní nemá (není prostá), pokud ji nezúžím

### Postup

1. přepíšu $y = f(x)$
2. **prohodím** $x$ a $y$
3. **vyjádřím** $y$
4. určím $D$ a $H$

---

## Vypočtené příklady

### 1) Vlastnosti mocninných funkcí

$y = x^{-3}$ (záporné liché)

- $D(f) = \mathbb{R} \setminus \{0\}$, $H(f) = \mathbb{R} \setminus \{0\}$
- lichá, klesající na $(-\infty;\, 0)$ i na $(0;\, \infty)$
- není omezená

$y = x^4$ (kladné sudé)

- $D(f) = \mathbb{R}$, $H(f) = \langle 0;\, \infty)$, sudá, minimum $0$ v bodě $x = 0$

### 2) Nerovnice s mocninami

$x^3 \geq x$

$x^3 - x \geq 0 \Rightarrow x(x-1)(x+1) \geq 0$

| interval | $x$ | $x-1$ | $x+1$ | součin |
|---|---|---|---|---|
| $(-\infty; -1)$ | − | − | − | − |
| $(-1; 0)$ | − | − | + | + |
| $(0; 1)$ | + | − | + | − |
| $(1; \infty)$ | + | + | + | + |

$x \in \langle -1;\, 0\rangle \cup \langle 1;\, \infty)$

### 3) Inverzní funkce – lineární

$f: y = 2x + 1$

1. prohodím: $x = 2y + 1$
2. vyjádřím $y$: $y = \dfrac{x - 1}{2}$

$f^{-1}(x) = \dfrac{x-1}{2}$

Kontrola: $f(3) = 7$ a $f^{-1}(7) = \dfrac{7-1}{2} = 3$ ✓

### 4) Inverzní funkce – třetí mocnina

$f: y = (x-1)^3 + 2$

1. prohodím: $x = (y-1)^3 + 2$
2. $(y-1)^3 = x - 2$
3. $y - 1 = \sqrt[3]{x-2}$

$f^{-1}(x) = \sqrt[3]{x-2} + 1$, $D = H = \mathbb{R}$

### 5) Inverzní funkce – lineární lomená

$f: y = \dfrac{1}{x} + 1$

1. prohodím: $x = \dfrac{1}{y} + 1$
2. $x - 1 = \dfrac{1}{y} \Rightarrow y = \dfrac{1}{x-1}$

$f^{-1}(x) = \dfrac{1}{x-1}$

- $D(f) = \mathbb{R} \setminus \{0\}$, $H(f) = \mathbb{R} \setminus \{1\}$
- $D(f^{-1}) = \mathbb{R} \setminus \{1\}$, $H(f^{-1}) = \mathbb{R} \setminus \{0\}$ (prohozené)

### 6) Funkce bez inverzní

$y = x^2$ na $\mathbb{R}$ **není prostá** ($f(2) = f(-2) = 4$), inverzní nemá.

Po zúžení na $\langle 0;\, \infty)$ už je prostá → $f^{-1}(x) = \sqrt{x}$.

---

**Souvisí:** [[01_Vlastnosti_funkci]], [[02_Linearni_lomena_funkce]], [[04_Exponencialni_funkce]], [[Matematika]]
