---
aliases: [unknown unicast, flooding]
tags: [slovnik]
---

# neznámý unicast

**Neznámý unicast** – rámec s [[unicast]] cílovou MAC adresou, kterou [[switch|přepínač]] nemá v tabulce. Přepošle ho proto na **všechny porty kromě příchozího**. Příklad: PC pošle rámec na MAC, která se ještě neozvala → switch ho rozešle všude, až cíl odpoví a switch se jeho MAC naučí.

---

## Podrobně

- důvod: [[CAM|tabulka MAC adres]] nemá pro cílovou MAC záznam,
- stejně se chovají [[broadcast]] a [[multicast]] (také jdou na všechny porty kromě příchozího),
- jakmile cíl odpoví, switch se z jeho zdrojové MAC naučí port a další rámce jdou už jen tam.

**Souvisí:** [[CAM]], [[switch]], [[unicast]], [[broadcast]], [[multicast]], [[Koncepty_prepinani]]
