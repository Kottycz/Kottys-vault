---
aliases: [SQLi, SQL injekce]
tags: [slovnik]
---

# SQL injection

Útok, kdy útočník vloží do formuláře **SQL kód** a databáze ho vykoná.

*Příklad: do přihlášení zadáš `' OR '1'='1` a přihlásíš se bez hesla.*

---

## Podrobně

- vzniká, když aplikace skládá SQL dotaz přímo ze vstupu uživatele
- obrana: **parametrizované dotazy**, kontrola vstupu
- takhle se stal únik Heartland (134 mil. karet)

**Souvisí:** [[zranitelnost]], [[exploit]]
