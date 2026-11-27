---
aliases: [SSH File Transfer Protocol, Secure FTP]
tags: [slovnik]
---

# SFTP

**SSH File Transfer Protocol** – zabezpečený přenos souborů přes [[SSH]]. Port **22**, běží nad [[TCP]].

---

## Podrobně

### Pozor na záměnu

Navzdory názvu **to není zabezpečená verze [[FTP]]** – je to úplně jiný protokol, který jen dělá totéž.

| Protokol | Co to je | Port |
| :-- | :-- | :-- |
| **[[FTP]]** | původní protokol, nešifrovaný | 20, 21 |
| **FTPS** | FTP zabalené do [[TLS]] | 990 |
| **SFTP** | přenos souborů **uvnitř [[SSH]]** | 22 |

### Výhody

- **Jediné spojení** na portu 22 – na rozdíl od FTP nepotřebuje zvlášť řídicí a datové spojení, takže bezproblémově prochází [[NAT|NATem]] a firewallem
- **Všechno šifrované** – jméno, heslo i obsah souborů
- Používá stejné ověřování jako SSH (heslo nebo klíč)
- Umí i výpis adresáře, mazání, přejmenování, práva

### Kde se s tím setkáš

- Nahrávání webu na server
- Zálohy a přenosy mezi servery
- Klienti: WinSCP, FileZilla, `sftp` v příkazové řádce

### SCP

Starší a jednodušší způsob kopírování přes SSH – umí jen kopírovat soubory, bez výpisu adresáře. SFTP je univerzálnější.

### Použití z příkazového řádku

```
C:\> sftp admin@192.168.1.100
sftp> ls
sftp> get zaloha.cfg
sftp> put novy.txt
sftp> bye
```

Grafičtí klienti: WinSCP, FileZilla (umí FTP i SFTP).

### Na Cisco

Router může fungovat jako SCP server (`ip scp server enable`) a soubory (IOS, konfigurace) se pak kopírují šifrovaně přes SSH místo nešifrovaného [[TFTP]].

**Souvisí:** [[SSH]], [[FTP]], [[TFTP]], [[TLS]], [[TCP]], [[port]]
