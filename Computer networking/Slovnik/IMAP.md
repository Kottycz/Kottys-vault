---
aliases: [Internet Message Access Protocol]
tags: [slovnik]
---

# IMAP

**Internet Message Access Protocol** – protokol pro **přístup k e-mailům přímo na serveru**. Port **143** (nešifrovaně), **993** (IMAPS). Pošta zůstává na serveru a synchronizuje se mezi zařízeními.

---

## Podrobně

### Jak funguje

Klient se serverem **synchronizuje stav schránky** – nestahuje ji natrvalo. Když si e-mail přečteš na mobilu, na počítači se taky zobrazí jako přečtený. Když ho přesuneš do složky, přesune se všude.

### Co umí navíc oproti POP3

- **Složky** – vytváření a správa složek na serveru
- **Stavy zpráv** – přečteno / nepřečteno / označeno hvězdičkou, synchronizované
- **Částečné stahování** – nejdřív jen hlavičky, přílohu až na vyžádání (šetří data)
- **Vyhledávání na serveru** – nemusí stahovat všechno

### IMAP vs. POP3

| | IMAP | [[POP3]] |
| :-- | :-- | :-- |
| Pošta zůstává | na serveru | v počítači |
| Synchronizace mezi zařízeními | ano | ne |
| Složky | ano | ne |
| Zátěž serveru | vyšší | nižší |
| Port | 143 / 993 | 110 / 995 |

### Kdy použít

Prakticky vždy, když čteš poštu z víc zařízení (mobil, notebook, web). Dnes standard.

### Pozor

Protože pošta zůstává na serveru, je omezená **kapacitou schránky** – při zaplnění přestanou chodit nové zprávy. A pokud server o data přijde, přijdeš o ně taky (pokud nemáš zálohu).

**Souvisí:** [[POP3]], [[SMTP]], [[TCP]], [[port]]
