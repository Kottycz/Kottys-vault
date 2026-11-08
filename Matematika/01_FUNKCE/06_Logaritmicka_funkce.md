---
aliases: [Logaritmická funkce, Logaritmus, Věty o logaritmech, Přirozený logaritmus]
tags: [matematika, funkce]
---

# Logaritmus a logaritmická funkce

## Definice

$$\log_a b = c \iff a^c = b \qquad (a > 0,\ a \neq 1,\ b > 0)$$

[[logaritmus]] $\log_a b$ je **číslo, na které musím umocnit $a$, aby vyšlo $b$**.

- $\log b$ = základ **10**
- $\ln b$ = základ **e** ≈ 2,718 ([[logaritmus|přirozený logaritmus]])

### Základní hodnoty

- $\log_a 1 = 0$
- $\log_a a = 1$
- $\log_a a^n = n$
- $a^{\log_a x} = x$

## Věty o logaritmech

| věta | vzorec |
|---|---|
| součin → součet | $\log_a (rs) = \log_a r + \log_a s$ |
| podíl → rozdíl | $\log_a \dfrac{r}{s} = \log_a r - \log_a s$ |
| mocnina → násobek | $\log_a r^n = n \cdot \log_a r$ |
| změna základu | $\log_a x = \dfrac{\log_b x}{\log_b a}$ |

**Všechny platí jen pro kladné $r$, $s$.** Nic jako $\log(r + s)$ se rozdělit nedá.

## Logaritmická funkce $y = \log_a x$

[[logaritmická funkce]] je **inverzní** k $y = a^x$ → graf je souměrný podle přímky $y = x$.

- $D(f) = (0;\, \infty)$
- $H(f) = \mathbb{R}$
- prochází bodem $[1;\, 0]$
- [[asymptota]]: osa y ($x = 0$)
- **a > 1** rostoucí, **0 < a < 1** klesající

## Řešení exponenciálních rovnic logaritmováním

Když nejde sjednotit základy: obě strany zlogaritmuju (třeba přes $\ln$) a mocnitel spadne dolů díky $\ln r^n = n \ln r$.

---

## Vypočtené příklady

### 1) Hodnoty logaritmů

- $\log_3 9 = 2$, protože $3^2 = 9$
- $\log_2 \tfrac18 = -3$, protože $2^{-3} = \tfrac18$
- $\log_4 32 = \tfrac52$, protože $4^{5/2} = (2^2)^{5/2} = 2^5 = 32$
- $\log_8 16 = \tfrac43$, protože $8^{4/3} = (2^3)^{4/3} = 2^4 = 16$
- $2^{\log_2 7} = 7$

### 2) Součet, rozdíl, násobek

$\log_2 64 - \log_5 125 + \log 0{,}01$

- $\log_2 64 = 6$ ($2^6$)
- $\log_5 125 = 3$ ($5^3$)
- $\log 0{,}01 = -2$ ($10^{-2}$)

$6 - 3 + (-2) = 1$

### 3) Zjednodušení pomocí vět

$\log_3 30 - \log_3 5 - \log_3 2$

$$= \log_3 \frac{30}{5 \cdot 2} = \log_3 3 = 1$$

### 4) Mocnina uvnitř

$3\log_3 2 - \log_3 24$

$$= \log_3 2^3 - \log_3 24 = \log_3 \frac{8}{24} = \log_3 \frac13 = -1$$

### 5) Změna základu

Vypočti $\log_2 3$ (kalkulačka umí jen $\log$ a $\ln$):

$$\log_2 3 = \frac{\ln 3}{\ln 2} = \frac{1{,}0986}{0{,}6931} \doteq 1{,}585$$

Kontrola: $2^{1{,}585} \doteq 3$ ✓

### 6) Graf, D, H, průsečíky

$f: y = \log_2 (x + 1) - 2$

- z $y = \log_2 x$: posun o **1 doleva** a **2 dolů**
- $D(f)$: $x + 1 > 0 \Rightarrow D(f) = (-1;\, \infty)$, $H(f) = \mathbb{R}$
- asymptota $x = -1$, rostoucí ($a = 2 > 1$)
- osa y: $y = \log_2 1 - 2 = -2$ → $[0;\, -2]$
- osa x: $\log_2 (x+1) = 2 \Rightarrow x + 1 = 4 \Rightarrow x = 3$ → $[3;\, 0]$

### 7) Exponenciální rovnice logaritmováním

$3^{x+1} = 2^{3-2x}$

1. zlogaritmuju: $(x+1)\ln 3 = (3 - 2x)\ln 2$
2. roznásobím: $x\ln 3 + \ln 3 = 3\ln 2 - 2x\ln 2$
3. $x$ na jednu stranu: $x(\ln 3 + 2\ln 2) = 3\ln 2 - \ln 3$

$$x = \frac{3\ln 2 - \ln 3}{\ln 3 + 2\ln 2} = \frac{\ln \tfrac83}{\ln 12} \doteq 0{,}3947$$

### 8) Exponenciální rovnice logaritmováním

$2 \cdot 3^{2x} = 5^{x-1}$

1. $\ln 2 + 2x\ln 3 = (x - 1)\ln 5$
2. $x(2\ln 3 - \ln 5) = -\ln 5 - \ln 2$

$$x = -\frac{\ln 10}{\ln \tfrac95} \doteq -3{,}917$$

---

**Souvisí:** [[04_Exponencialni_funkce]], [[05_Exponencialni_rovnice]], [[07_Logaritmicke_rovnice]], [[Matematika]]
