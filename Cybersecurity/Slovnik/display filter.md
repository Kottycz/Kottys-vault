---
aliases: [zobrazovací filtr, display filtr]
tags: [slovnik]
---

# display filter

Filtr, který jen **skryje pakety**, které mu neodpovídají – nic nemaže a dá se měnit kdykoli.

*Příklad: `http.request.method == "POST"` – ukáže jen HTTP POST požadavky.*

---

## Podrobně

- píše se do **lišty filtru** nad seznamem paketů
- syntaxe `protokol.pole operátor hodnota`, **malými písmeny**
- operátory `==`, `!=`, `>`, `<`, `and`, `or`, `!`, `contains`, `matches`, `in`
- barva lišty: **zelená** platný, **červená** neplatný, **žlutá** nespolehlivý
- ~3000 protokolů; průvodce **Analyse → Display Filter Expression**
- počet zobrazených paketů je ve stavovém řádku
- pravý klik na pole → **Apply as Filter**

**Souvisí:** [[capture filter]], [[Wireshark]], [[Wireshark příkazy]]
