---
aliases: [Post Office Protocol 3]
tags: [slovnik]
---

# POP3

**Post Office Protocol version 3** – protokol pro **stahování** e-mailů ze serveru. Port **110** (nešifrovaně), **995** (POP3S). Zprávy typicky stáhne a ze serveru smaže.

---

## Podrobně

### Jak funguje

1. Klient se připojí k serveru
2. Stáhne všechny nové zprávy do počítače
3. Ve výchozím nastavení je ze serveru **smaže**
4. Odpojí se

Pošta pak existuje jen lokálně na tom jednom zařízení.

### POP3 vs. IMAP

| | POP3 | [[IMAP]] |
| :-- | :-- | :-- |
| Kde je pošta | stažená v počítači | na serveru |
| Víc zařízení | ne (každé vidí jinou poštu) | ano (vše synchronizované) |
| Složky | ne | ano |
| Offline přístup | ano (je lokálně) | jen stažené/cache |
| Zátěž serveru | nízká | vyšší (drží všechnu poštu) |
| Port | 110 / 995 | 143 / 993 |

### Kdy dává smysl

- Pošta se čte jen z jednoho zařízení
- Malá kapacita schránky na serveru
- Chceš mít všechno lokálně u sebe

Dnes většina lidí používá víc zařízení (mobil + počítač), proto se běžně volí [[IMAP]].

### Zabezpečení

Základní POP3 posílá heslo i obsah **nešifrovaně**. Používej POP3S (port 995) nebo STARTTLS.

### Průběh relace

1. klient se připojí na port 110 (nebo 995),
2. přihlásí se (`USER`, `PASS`),
3. stáhne zprávy (`LIST`, `RETR`),
4. označí je ke smazání (`DELE`),
5. `QUIT` – server označené zprávy smaže.

### Proč dnes převládá IMAP

Uživatelé mají e-mail na mobilu, notebooku i ve webovém rozhraní. POP3 zprávy stáhne na jedno zařízení a ze serveru smaže, takže na ostatních chybí. [[IMAP]] drží vše na serveru a synchronizuje stav.

**Souvisí:** [[IMAP]], [[SMTP]], [[TCP]], [[port]]
