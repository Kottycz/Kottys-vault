---
aliases: [Exponenciální rovnice]
tags: [matematika, rovnice]
---

# Exponenciální rovnice

Rovnice, kde je **neznámá v exponentu**. Funkce $a^x$ je [[prostá funkce|prostá]], takže:

$$a^{u} = a^{v} \iff u = v$$

## Postupy (od nejjednoduššího)

1. **Stejný základ** – obě strany upravím na mocniny stejného čísla, pak porovnám exponenty.
2. **Vytknutí** – když je mezi mocninami $+$ nebo $-$, vytknu nejmenší mocninu: $2^{x+1} = 2 \cdot 2^x$.
3. **[[substituce]]** – $t = a^x$, vznikne (kvadratická) rovnice v $t$. **Pozor: $t > 0$**, záporné kořeny zahodit.
4. **Dělení** – různé základy (např. $4^x, 6^x, 9^x$): vydělím jednou z mocnin a substituuju podíl.
5. **Logaritmování** – když to nejde na stejný základ, viz [[06_Logaritmicka_funkce]].

## Vzorce pro mocniny (opakování)

- $a^m \cdot a^n = a^{m+n}$
- $\dfrac{a^m}{a^n} = a^{m-n}$
- $(a^m)^n = a^{mn}$
- $a^{-n} = \dfrac{1}{a^n}$
- $(ab)^x = a^x b^x$

---

## Vypočtené příklady

### 1) Stejný základ

$9^{x-2} = 27 \cdot 3^{4-x}$

1. vše na základ 3: $3^{2x-4} = 3^3 \cdot 3^{4-x} = 3^{7-x}$
2. porovnám exponenty: $2x - 4 = 7 - x$
3. $3x = 11$

$x = \dfrac{11}{3}$

### 2) Vytknutí

$3 \cdot 2^x + 2^x = 32$

$2^x(3 + 1) = 32 \Rightarrow 4 \cdot 2^x = 32 \Rightarrow 2^x = 8$

$x = 3$

### 3) Úprava a vytknutí

$2 \cdot 3^x + 3^{x+1} = 5$

1. $3^{x+1} = 3 \cdot 3^x$
2. $2 \cdot 3^x + 3 \cdot 3^x = 5 \cdot 3^x = 5$
3. $3^x = 1$

$x = 0$

### 4) Substituce

$2 \cdot 4^x - 9 \cdot 2^x + 4 = 0$

1. $4^x = (2^x)^2$, zavedu $t = 2^x > 0$
2. $2t^2 - 9t + 4 = 0$
3. $D = 81 - 32 = 49$, $t = \dfrac{9 \pm 7}{4}$ → $t = 4$ nebo $t = \tfrac12$ (obojí je kladné ✓)
4. $2^x = 4 \Rightarrow x = 2$; $2^x = \tfrac12 \Rightarrow x = -1$

$x \in \{-1;\, 2\}$

Zkouška $x = 2$: $2 \cdot 16 - 9 \cdot 4 + 4 = 32 - 36 + 4 = 0$ ✓

### 5) Různé základy – spojení do jednoho

$3^x \cdot 2^{x+1} = 72$

1. $2^{x+1} = 2 \cdot 2^x$ → $2 \cdot 3^x \cdot 2^x = 2 \cdot 6^x = 72$
2. $6^x = 36$

$x = 2$

### 6) Dělení a substituce

$9^{x+1} + 5 \cdot 6^x = 4^{x+1}$

1. rozepíšu: $9 \cdot 9^x + 5 \cdot 6^x = 4 \cdot 4^x$
2. vydělím $4^x$: $9 \cdot \left(\tfrac94\right)^x + 5 \cdot \left(\tfrac32\right)^x = 4$
3. $t = \left(\tfrac32\right)^x > 0$, pak $\left(\tfrac94\right)^x = t^2$: $9t^2 + 5t - 4 = 0$
4. $D = 25 + 144 = 169$, $t = \dfrac{-5 \pm 13}{18}$ → $t = \tfrac49$ nebo $t = -1$ (**záporné zahodit**)
5. $\left(\tfrac32\right)^x = \tfrac49 = \left(\tfrac32\right)^{-2}$

$x = -2$

Zkouška: $9^{-1} + 5 \cdot 6^{-2} = \tfrac19 + \tfrac{5}{36} = \tfrac{9}{36} = \tfrac14 = 4^{-1}$ ✓

---

**Souvisí:** [[04_Exponencialni_funkce]], [[06_Logaritmicka_funkce]], [[07_Logaritmicke_rovnice]], [[Matematika]]
