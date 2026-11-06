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

**Souvisí:** [[firewall]], [[SSH]], [[IOS]]
