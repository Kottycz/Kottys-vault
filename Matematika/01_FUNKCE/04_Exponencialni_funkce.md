---
aliases: [Exponenciální funkce]
tags: [matematika, funkce]
---

# Exponenciální funkce

Tvar: $y = a^x$, kde **a > 0** a **a ≠ 1** ([[exponenciální funkce]]).

**Proč tyhle podmínky:** základ musí jít umocnit na *jakékoliv* číslo. Záporný základ nejde ($(-2)^{1/2}$ neexistuje), $a = 1$ dává jen konstantu 1, $a = 0$ také.

## Vlastnosti

- $D(f) = \mathbb{R}$
- $H(f) = (0;\, \infty)$ – hodnoty jsou **vždy kladné**
- prochází bodem $[0;\, 1]$ (protože $a^0 = 1$)
- [[asymptota]]: osa x ($y = 0$), graf se k ní blíží, ale nedotkne se
- [[prostá funkce]], není sudá ani lichá, není omezená shora (zdola ano, číslem 0)
- **nemá** průsečík s osou x

| | **a > 1** | **0 < a < 1** |
|---|---|---|
| monotonie | rostoucí | klesající |
| pro $x \to \infty$ | $y \to \infty$ | $y \to 0$ |
| pro $x \to -\infty$ | $y \to 0$ | $y \to \infty$ |

Graf $y = \left(\tfrac1a\right)^x = a^{-x}$ je souměrný s grafem $y = a^x$ podle **osy y**.

## Posuny grafu

- $y = a^{x + c}$ – posun o $c$ **doleva** (pro $c < 0$ doprava)
- $y = a^x + d$ – posun o $d$ **nahoru**, asymptota $y = d$

## Porovnávání čísel

- základ **> 1**: větší exponent → větší číslo
- základ **0 až 1**: větší exponent → **menší** číslo

---

## Vypočtené příklady

### 1) Graf, D, H, asymptota

$f: y = 2^{x-1} + 3$

- z $y = 2^x$: posun o **1 doprava** a **3 nahoru**
- asymptota $y = 3$
- $D(f) = \mathbb{R}$, $H(f) = (3;\, \infty)$
- průsečík s osou y: $y = 2^{-1} + 3 = 3{,}5$ → $[0;\, 3{,}5]$
- s osou x: **žádný** (všechny hodnoty jsou větší než 3)

### 2) Seřazení čísel

Seřaď vzestupně: $\left(\tfrac12\right)^3,\ \left(\tfrac12\right)^{-2},\ \left(\tfrac12\right)^0,\ \left(\tfrac12\right)^1$

Spočítám: $\tfrac18,\ 4,\ 1,\ \tfrac12$

$$\left(\tfrac12\right)^3 < \left(\tfrac12\right)^1 < \left(\tfrac12\right)^0 < \left(\tfrac12\right)^{-2}$$

Zdůvodnění: základ je $\tfrac12 < 1$ → funkce **klesá**, takže největší exponent dá nejmenší číslo.

### 3) Porovnání bez kalkulačky

Porovnej $\left(\tfrac23\right)^{-0{,}5}$ a $\left(\tfrac23\right)^{0{,}2}$.

Základ $\tfrac23 < 1$ → klesající. $-0{,}5 < 0{,}2$, proto

$$\left(\tfrac23\right)^{-0{,}5} > \left(\tfrac23\right)^{0{,}2}$$

### 4) Parametr v základu

Pro která $p$ je $y = (2p - 3)^x$ rostoucí, klesající, nebo to není exponenciální funkce?

- **rostoucí:** $2p - 3 > 1 \Rightarrow p > 2$
- **klesající:** $0 < 2p - 3 < 1 \Rightarrow \tfrac32 < p < 2$
- **není exponenciální:** $2p - 3 \leq 0$ nebo $2p - 3 = 1$, tj. $p \leq \tfrac32$ nebo $p = 2$

---

**Souvisí:** [[03_Mocninna_funkce]], [[05_Exponencialni_rovnice]], [[06_Logaritmicka_funkce]], [[Matematika]]
