---
aliases: [File Transfer Protocol]
tags: [slovnik]
---

# FTP

**File Transfer Protocol** – protokol pro přenos souborů mezi klientem a serverem. Používá **dvě** [[TCP]] spojení: port **21** (řízení) a **20** (data).

---

## Podrobně

### Dvě spojení

FTP je nezvyklý tím, že odděluje příkazy od dat:

| Spojení | Port | K čemu |
| :-- | :-- | :-- |
| **Řídicí** | 21 | příkazy (LIST, GET, PUT), přihlášení – drží se otevřené celou relaci |
| **Datové** | 20 nebo dynamický | samotný obsah souboru – otevírá se pro každý přenos |

### Aktivní vs. pasivní režim

- **Aktivní** – datové spojení navazuje **server** směrem ke klientovi. Nefunguje, když je klient za [[NAT]] nebo firewallem (spojení dovnitř se zablokuje).
- **Pasivní (PASV)** – datové spojení navazuje **klient**. Dnes běžnější, protože prochází NATem.

### Bezpečnost – hlavní problém

Klasické FTP posílá **jméno, heslo i obsah souborů nešifrovaně**. Kdokoliv po cestě to může odposlechnout. Proto se používají náhrady:

| Protokol | Popis | Port |
| :-- | :-- | :-- |
| **FTPS** | FTP + TLS šifrování | 990 |
| **SFTP** | přenos souborů přes SSH (jiný protokol, ne FTP!) | 22 |
| **TFTP** | zjednodušený, nad [[UDP]], bez ověřování – pro zavádění konfigurací síťových prvků | 69 |

### Anonymní FTP

Veřejné servery umožňují přihlášení jménem `anonymous` – používalo se pro distribuci softwaru, dnes už spíš historie.

**Souvisí:** [[TCP]], [[port]], [[NAT]], [[UDP]]
