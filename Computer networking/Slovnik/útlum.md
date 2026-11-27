---
aliases: [útlum, attenuation, útlum signálu]
tags: [slovnik]
---

# útlum (attenuation)

**Útlum** – slábnutí signálu, čím delší cestu po médiu urazí.

*Příklad: příliš dlouhý UTP kabel (přes 100 m) → signál je na konci tak slabý, že se data poškodí.*

---

## Podrobně

- týká se všech médií: měď, optika, bezdrát
- proto mají standardy kabeláže **maximální délky kabelů** (UTP = 100 m)
- řešení na delší vzdálenosti: zesilovač, switch, přechod na [[optické vlákno]]
- další problémy fyzické vrstvy: rušení [[EMI]] / RFI, přeslech (crosstalk)

### Jak se útlum měří

Útlum se udává v **decibelech (dB)**. Každé zvýšení útlumu o 3 dB znamená zhruba poloviční výkon signálu. U kabeláže se měří certifikačním měřákem, který ověří, že linka splňuje kategorii.

### Maximální délky

| Médium | Max. délka |
| :-- | :-- |
| [[UTP]] (Ethernet) | **100 m** (90 m pevná kabeláž + 10 m patch kabely) |
| multimode optika (1 Gb/s) | stovky metrů |
| single-mode optika | desítky km |

### Co zvyšuje útlum

- délka kabelu,
- vyšší frekvence (rychlejší přenos = větší útlum),
- špatné konektory a spoje,
- u optiky ohyby vlákna a znečištěné konektory,
- u Wi-Fi zdi, vzdálenost, překážky.

**Souvisí:** [[UTP]], [[EMI]], [[optické vlákno]]
