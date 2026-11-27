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

### Záloha a obnova přes TFTP

```
R1# copy running-config tftp:
Address or name of remote host []? 192.168.1.100
Destination filename [r1-confg]? r1-zaloha.cfg

R1# copy tftp: running-config
```

Na PC musí běžet TFTP server (např. Tftpd64) a mezi zařízením a PC musí fungovat ping.

### Omezení

- soubory se posílají po blocích **512 B**, každý blok se potvrzuje, takže je TFTP pomalé,
- bez přihlášení a bez šifrování → jen v uzavřené síti pro správu,
- neumí vypsat obsah adresáře, musíš znát přesný název souboru.

### Bezpečnější alternativa

SCP nebo [[SFTP]] přes SSH (`copy running-config scp:`).

**Souvisí:** [[FTP]], [[UDP]], [[port]], [[running-config]], [[startup-config]]
