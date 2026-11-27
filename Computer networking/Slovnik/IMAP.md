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

### Porty

| Port | Protokol | Šifrování |
| :-- | :-- | :-- |
| 143 | IMAP | ne (nebo STARTTLS) |
| 993 | IMAPS | [[TLS]] |
| 110 / 995 | [[POP3]] / POP3S | ne / ano |
| 25 / 587 / 465 | [[SMTP]] | odesílání, různé varianty |

### Celý tok e-mailu

1. klient pošle e-mail svému serveru přes **SMTP**,
2. server ho přes SMTP předá serveru příjemce,
3. příjemce si ho přečte přes **IMAP** (nebo POP3).

IMAP a POP3 slouží jen ke **čtení**, odesílá se vždy přes SMTP.

### Složky a stavy

IMAP drží na serveru i složky (Doručené, Odeslané, vlastní složky) a příznaky (přečteno, označeno). Proto vidíš stejný stav na mobilu i v počítači.

**Souvisí:** [[POP3]], [[SMTP]], [[TCP]], [[port]]
