---
aliases: [Content Addressable Memory, tabulka MAC adres, tabulka CAM, MAC address table]
tags: [slovnik]
---

# CAM

**CAM** (Content Addressable Memory) – rychlá paměť v [[switch|přepínači]], kde je uložená **tabulka MAC adres** (která [[MAC adresa]] je na kterém portu). Příklad: PC s MAC `AA:BB:..` je na portu Fa0/3 → rámec pro něj jde jen ven z Fa0/3.

---

## Podrobně

- speciální paměť pro **vysokorychlostní vyhledávání** (hledá se podle obsahu, ne podle adresy),
- proto se tabulce MAC adres říká i **tabulka CAM**,
- jedna hlavní tabulka na switch: rámec s danou cílovou MAC vždy odchází stejným portem,
- učí se ze **zdrojové MAC** příchozích rámců, položka vyprší po **5 minutách** bez provozu (výchozí),
- není-li cíl v tabulce, jde rámec všude kromě příchozího portu ([[neznámý unicast]]).

**Souvisí:** [[switch]], [[MAC adresa]], [[neznámý unicast]], [[Koncepty_prepinani]]
