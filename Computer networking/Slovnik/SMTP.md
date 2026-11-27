---
aliases: [Simple Mail Transfer Protocol]
tags: [slovnik]
---

# SMTP

**Simple Mail Transfer Protocol** – protokol pro **odesílání** e-mailů. Port **25** (mezi servery), **587** (od klienta, s šifrováním). Běží nad [[TCP]].

---

## Podrobně

### Role v e-mailu

SMTP e-maily jen **posílá a doručuje mezi servery**. Pro jejich stažení a čtení slouží [[POP3]] nebo [[IMAP]].

```
Odesílatel ──SMTP──► server A ──SMTP──► server B ──POP3/IMAP──► Příjemce
```

### Jak najde cílový server

Podle domény v adrese (`@seznam.cz`) se zeptá [[DNS]] na **MX záznam** – ten říká, který server přijímá poštu pro tuhle doménu.

### Porty

| Port | Použití |
| :-- | :-- |
| **25** | mezi servery (často blokován ISP kvůli spamu) |
| **587** | odesílání od klienta, s STARTTLS |
| **465** | odesílání přes SMTPS (celé spojení šifrované) |

### Zabezpečení

Původní SMTP neměl žádné ověřování – kdokoliv mohl poslat e-mail jménem kohokoliv. Proto dnes:

- **SMTP AUTH** – přihlášení jménem a heslem před odesláním
- **STARTTLS** – šifrování spojení
- **SPF, DKIM, DMARC** – DNS záznamy, které ověřují, že server smí posílat za danou doménu (obrana proti podvržení odesílatele)

### Jak vypadá SMTP relace

```
S: 220 mail.skola.cz ESMTP
C: HELO pc.skola.cz
C: MAIL FROM:<jan@skola.cz>
C: RCPT TO:<petr@seznam.cz>
C: DATA
C: Subject: Test
C: Ahoj.
C: .
S: 250 OK
C: QUIT
```

Server odpovídá číselnými kódy: 2xx = OK, 4xx = dočasná chyba (zkus později), 5xx = trvalá chyba (třeba neexistující adresa).

### Ochrana proti spamu

- **SPF** – záznam v [[DNS]], které servery smí posílat poštu za doménu,
- **DKIM** – digitální podpis e-mailu,
- **DMARC** – co dělat se zprávou, která neprojde SPF nebo DKIM.

Bez nich se dá snadno podvrhnout odesílatel.

**Souvisí:** [[POP3]], [[IMAP]], [[DNS]], [[TCP]], [[port]]
