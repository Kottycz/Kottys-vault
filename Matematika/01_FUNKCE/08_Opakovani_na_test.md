---
aliases: [Opakování na test, Opakování funkce, Test funkce]
tags: [matematika, funkce, opakovani]
---

# Opakování na test – funkce

U každého tématu: **vzorec → graf → jeden příklad, ze kterého graf vzejde.**
Podrobně viz zápisky [[01_Vlastnosti_funkci]] až [[07_Logaritmicke_rovnice]].

---

## 1) Vlastnosti funkcí – kvadratická funkce

**Vzorec**

- $y = ax^2 + bx + c$ → doplnění na čtverec → $y = a(x - m)^2 + n$, vrchol $V[m;\, n]$
- $a > 0$ minimum, $a < 0$ maximum
- $D(f)$: jmenovatel $\neq 0$, pod odmocninou $\geq 0$, v logaritmu $> 0$
- sudá $f(-x) = f(x)$, lichá $f(-x) = -f(x)$

**Graf**

![[01_kvadraticka.png]]

**Příklad:** nakresli $y = x^2 - 4x + 1$

1. doplním na čtverec: $y = (x - 2)^2 - 4 + 1 = (x - 2)^2 - 3$
2. vrchol $V[2;\, -3]$, $a = 1 > 0$ → otevřená nahoru, $H(f) = \langle -3;\, \infty)$
3. osa y ($x = 0$): $y = 1$ → $[0;\, 1]$
4. osa x ($y = 0$): $(x - 2)^2 = 3 \Rightarrow x = 2 \pm \sqrt{3}$
5. klesající na $(-\infty;\, 2\rangle$, rostoucí na $\langle 2;\, \infty)$

---

## 2) Lineární lomená funkce

**Vzorec**

- $y = \dfrac{k}{x - a} + b$ → střed $S[a;\, b]$, asymptoty $x = a$, $y = b$
- $D(f) = \mathbb{R} \setminus \{a\}$, $H(f) = \mathbb{R} \setminus \{b\}$
- $k > 0$ klesající na obou intervalech, $k < 0$ rostoucí
- úprava: v čitateli udělat násobek jmenovatele + zbytek

**Graf**

![[02_linearni_lomena.png]]

**Příklad:** nakresli $y = \dfrac{3x + 1}{x - 1}$

1. upravím čitatel: $3x + 1 = 3(x - 1) + 4$
2. $y = \dfrac{3(x-1) + 4}{x - 1} = 3 + \dfrac{4}{x - 1}$
3. $k = 4 > 0$, střed $S[1;\, 3]$, asymptoty $x = 1$ a $y = 3$
4. $D(f) = \mathbb{R} \setminus \{1\}$, $H(f) = \mathbb{R} \setminus \{3\}$
5. osa y: $y = \dfrac{1}{-1} = -1$ → $[0;\, -1]$
6. osa x: $3x + 1 = 0 \Rightarrow x = -\tfrac13$ → $[-\tfrac13;\, 0]$

---

## 3) Mocninná a inverzní funkce

**Vzorec**

- $y = x^n$: **n sudé** – $H = \langle 0; \infty)$, sudá; **n liché** – $H = \mathbb{R}$, lichá, rostoucí
- $y = x^{-n}$: $D = \mathbb{R} \setminus \{0\}$, asymptoty osy
- inverzní funkce: **prohodit $x$ a $y$ a vyjádřit $y$**
- $D(f^{-1}) = H(f)$, $H(f^{-1}) = D(f)$, graf souměrný podle $y = x$
- inverzní existuje jen k **prosté** funkci

**Graf**

![[03_mocninna_inverzni.png]]

**Příklad:** najdi inverzní funkci k $f: y = (x - 1)^3 + 2$ a nakresli obě

1. prohodím: $x = (y - 1)^3 + 2$
2. $(y - 1)^3 = x - 2$
3. $y - 1 = \sqrt[3]{x - 2}$
4. $f^{-1}: y = \sqrt[3]{x - 2} + 1$, $D = H = \mathbb{R}$
5. $f$ je $x^3$ posunutá o $1$ doprava a $2$ nahoru; $f^{-1}$ je její obraz podle přímky $y = x$ (bod $[2;\, 3]$ z $f$ → bod $[3;\, 2]$ na $f^{-1}$)

---

## 4) Exponenciální funkce

**Vzorec**

- $y = a^x$, $a > 0$, $a \neq 1$
- $D(f) = \mathbb{R}$, $H(f) = (0;\, \infty)$, prochází $[0;\, 1]$, asymptota $y = 0$
- $a > 1$ rostoucí, $0 < a < 1$ klesající
- $y = a^{x + c} + d$: posun o $c$ doleva, o $d$ nahoru, asymptota $y = d$

**Graf**

![[04_exponencialni.png]]

**Příklad:** nakresli $y = 2^{x-1} + 3$

1. vyjdu z $y = 2^x$ (rostoucí, $a = 2 > 1$)
2. $x - 1$ → posun o **1 doprava**; $+3$ → posun o **3 nahoru**
3. asymptota $y = 3$
4. $D(f) = \mathbb{R}$, $H(f) = (3;\, \infty)$
5. osa y: $2^{-1} + 3 = 3{,}5$ → $[0;\, 3{,}5]$
6. průsečík s osou x **není** (hodnoty jsou vždy $> 3$)

---

## 5) Exponenciální rovnice

**Vzorec**

- $a^u = a^v \iff u = v$ (stejný základ → porovnat exponenty)
- $a^{x + n} = a^n \cdot a^x$, $a^{-x} = \dfrac{1}{a^x}$, $4^x = (2^x)^2$
- **substituce** $t = a^x$, **$t > 0$**
- různé základy → dělení, nebo logaritmování

**Graf** (kořeny rovnice = průsečíky grafu s osou x)

![[05_exponencialni_rovnice.png]]

**Příklad:** vyřeš $2 \cdot 4^x - 9 \cdot 2^x + 4 = 0$ (graf je funkce na levé straně)

1. $4^x = (2^x)^2$, zavedu $t = 2^x > 0$
2. $2t^2 - 9t + 4 = 0$, $D = 81 - 32 = 49$
3. $t = \dfrac{9 \pm 7}{4}$ → $t = 4$ nebo $t = \tfrac12$ (obojí kladné ✓)
4. $2^x = 4 \Rightarrow x = 2$; $2^x = \tfrac12 \Rightarrow x = -1$
5. graf protíná osu x přesně v $x = -1$ a $x = 2$

---

## 6) Logaritmická funkce

**Vzorec**

- $\log_a b = c \iff a^c = b$ ($a > 0$, $a \neq 1$, $b > 0$)
- $\log_a (rs) = \log_a r + \log_a s$, $\log_a \dfrac{r}{s} = \log_a r - \log_a s$, $\log_a r^n = n\log_a r$
- změna základu $\log_a x = \dfrac{\ln x}{\ln a}$
- $y = \log_a x$: $D = (0;\, \infty)$, $H = \mathbb{R}$, prochází $[1;\, 0]$, asymptota $x = 0$, inverzní k $a^x$

**Graf**

![[06_logaritmicka.png]]

**Příklad:** nakresli $y = \log_2 (x + 1) - 2$

1. vyjdu z $y = \log_2 x$ (rostoucí, $a = 2 > 1$)
2. $x + 1$ → posun o **1 doleva**; $-2$ → posun o **2 dolů**
3. asymptota $x = -1$, $D(f) = (-1;\, \infty)$, $H(f) = \mathbb{R}$
4. osa y: $\log_2 1 - 2 = -2$ → $[0;\, -2]$
5. osa x: $\log_2 (x + 1) = 2 \Rightarrow x + 1 = 4 \Rightarrow x = 3$ → $[3;\, 0]$

---

## 7) Logaritmické rovnice

**Vzorec**

- **nejdřív podmínky:** každý argument logaritmu $> 0$
- $\log_a f = c \Rightarrow f = a^c$
- $\log_a f = \log_a g \Rightarrow f = g$
- součet / rozdíl logaritmů → **jeden logaritmus**
- $\log^2 x$ → substituce $t = \log x$
- **zkouška / kontrola podmínek** nakonec

**Graf** (levá strana rovnice a pravá strana $y = 1$)

![[07_logaritmicka_rovnice.png]]

**Příklad:** vyřeš $\log_2 x + \log_2 (x - 1) = 1$

1. podmínky: $x > 0$ a $x - 1 > 0$ → $x > 1$
2. spojím: $\log_2 [x(x - 1)] = 1 \Rightarrow x(x - 1) = 2^1 = 2$
3. $x^2 - x - 2 = 0 \Rightarrow (x - 2)(x + 1) = 0$
4. $x = 2$ ✓, $x = -1$ ✗ (**není $> 1$**, graf v něm vůbec neexistuje)

$x = 2$ – průsečík grafu s přímkou $y = 1$

---

**Souvisí:** [[Matematika]]
