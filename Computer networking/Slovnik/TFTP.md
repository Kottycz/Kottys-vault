---
aliases: [Trivial File Transfer Protocol]
tags: [slovnik]
---

# TFTP

**Trivial File Transfer Protocol** – zjednodušený protokol pro přenos souborů. Běží nad [[UDP]] na portu **69**, nemá žádné ověřování.

---

## Podrobně

### Čím se liší od FTP

| | TFTP | [[FTP]] |
| :-- | :-- | :-- |
| Protokol | [[UDP]] | [[TCP]] |
| Port | 69 | 20, 21 |
| Přihlášení | **žádné** | jméno + heslo |
| Výpis adresáře | ne | ano |
| Složitost | minimální | plnohodnotný |

TFTP umí jen dvě věci: **stáhnout soubor** a **nahrát soubor**. Nic víc.

### Kde se používá

- **Zálohování konfigurací** síťových prvků:
  ```
  Router# copy running-config tftp:
  ```
- **Nahrávání IOS** (firmwaru) do [[router|routerů]] a [[switch|switchů]]
- **Bootování zařízení po síti** (PXE boot) – tenké klienty, IP telefony

Používá se tam, kde je potřeba jednoduchý klient, který se vejde do malé paměti zařízení.

### Bezpečnost

Žádná. Nemá ověřování ani šifrování – kdokoliv, kdo zná název souboru, si ho může stáhnout. Proto se používá **jen ve vnitřní správcovské síti**, nikdy přes internet.

### Spolehlivost

Přestože jede nad nespolehlivým UDP, řeší si potvrzování sám – každý blok dat potvrzuje příjemce vlastní ACK zprávou.

**Souvisí:** [[FTP]], [[UDP]], [[port]], [[running-config]], [[startup-config]]
