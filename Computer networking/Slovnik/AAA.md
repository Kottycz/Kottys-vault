---
aliases: [Authentication Authorization Accounting, triple A]
tags: [slovnik]
---

# AAA

**Authentication, Authorization, Accounting** ("triple A") – primární rámec pro nastavení řízení přístupu na síťových zařízeních.

---

## Podrobně

### Tři složky

| Složka | Otázka | Co dělá |
| :-- | :-- | :-- |
| **Authentication** (ověřování) | "Kdo jsi?" | ověří identitu uživatele (jméno + heslo, certifikát…) |
| **Authorization** (autorizace) | "Co smíš dělat?" | určí, k čemu má ověřený uživatel přístup |
| **Accounting** (účtování) | "Co jsi dělal?" | loguje aktivitu uživatele pro pozdější audit |

### Proč se dělá dohromady

Samotné ověření identity nestačí – je potřeba i řídit, co uživatel smí (autorizace), a mít záznam, co skutečně udělal (účtování), pro zpětnou kontrolu a odhalení zneužití.

### Kde se používá

Přihlašování do síťových zařízení (routery, switche), VPN, podnikové sítě – často realizováno přes centrální server (RADIUS, TACACS+).

### Lokální vs. serverová AAA

- **lokální** – uživatelé a hesla jsou přímo v konfiguraci zařízení (`username admin secret heslo`). Jednoduché, ale u 50 switchů musíš měnit heslo na každém zvlášť,
- **serverová** – zařízení se ptá centrálního serveru. Jedno místo pro všechny účty, dá se logovat, kdo co udělal.

### RADIUS vs. TACACS+

| | RADIUS | TACACS+ |
| :-- | :-- | :-- |
| standard | otevřený ([[IETF]]) | Cisco |
| transport | [[UDP]] 1812/1813 | [[TCP]] 49 |
| šifrování | jen heslo | celé tělo zprávy |
| AAA | autentizace a autorizace dohromady | všechny tři části zvlášť |
| typické použití | Wi-Fi, VPN, síťový přístup uživatelů | správa síťových zařízení (kdo smí jaký příkaz) |

### Základní konfigurace (lokální)

```
R1(config)# username admin secret Cisco123
R1(config)# aaa new-model
R1(config)# aaa authentication login default local
R1(config)# line vty 0 4
R1(config-line)# login authentication default
```

`aaa new-model` zapne AAA. Od té chvíle se přihlášení řídí AAA, ne starým příkazem `login`.

### Accounting v praxi

Záznam o tom, **kdo se kdy přihlásil a jaké příkazy zadal**. Když se něco v síti rozbije, dohledá se, kdo změnil konfiguraci.

**Souvisí:** [[firewall]], [[SSH]], [[IOS]]
