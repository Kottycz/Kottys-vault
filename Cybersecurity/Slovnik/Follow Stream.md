---
aliases: [Follow TCP Stream, Follow UDP Stream, Follow HTTP Stream]
tags: [slovnik]
---

# Follow Stream

Funkce Wiresharku, která **složí pakety zpět do dat aplikace** – vidíš celou konverzaci jako text.

*Příklad: pravý klik na HTTP paket → Follow → TCP Stream ukáže GET i odpověď serveru.*

---

## Podrobně

- **Analyse → Follow → TCP / UDP / HTTP / TLS Stream** nebo `Ctrl+Alt+Shift+T`
- **klient červeně**, **server modře**
- je vidět nešifrovaný obsah – jména, hesla, soubory
- automaticky nastaví filtr `tcp.stream eq N` → zrušit tlačítkem **X**
- formáty: ASCII, EBCDIC, Hex Dump, C Arrays, Raw
- **Save as** = uložit text, **Filter Out This Stream** = skrýt stream
- u HTTPS bez klíčů jen nečitelná data

**Souvisí:** [[Wireshark]], [[display filter]], [[HTTP]]
