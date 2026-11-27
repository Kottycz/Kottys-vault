---
aliases: [Transport Layer Security, SSL, Secure Sockets Layer]
tags: [slovnik]
---

# TLS

**Transport Layer Security** – protokol pro šifrování komunikace. Zajišťuje důvěrnost, integritu a ověření identity serveru. Nástupce staršího **SSL**.

---

## Podrobně

### Kde se používá

TLS je vrstva mezi [[TCP]] a aplikačním protokolem – proto "S" v názvech zabezpečených protokolů:

| Protokol | Bez TLS | S TLS | Port |
| :-- | :-- | :-- | :-- |
| Web | [[HTTP]] | **[[HTTPS]]** | 443 |
| E-mail (odesílání) | [[SMTP]] | SMTPS | 465 |
| E-mail (stahování) | [[POP3]] | POP3S | 995 |
| E-mail (přístup) | [[IMAP]] | IMAPS | 993 |
| Přenos souborů | [[FTP]] | FTPS | 990 |

### Co zajišťuje

1. **Šifrování** – nikdo po cestě nepřečte obsah
2. **Integrita** – data nelze cestou změnit
3. **Autenticita** – certifikát ověří, že server je ten pravý

### Handshake (zjednodušeně)

```
1. Klient pošle, jaké šifry umí
2. Server pošle certifikát s veřejným klíčem
3. Klient ověří certifikát u certifikační autority (CA)
4. Dohodnou se na symetrickém klíči relace
5. Dál už jde všechno šifrovaně
```

### Verze

| Verze | Stav |
| :-- | :-- |
| SSL 2.0, 3.0 | **nebezpečné**, zakázané |
| TLS 1.0, 1.1 | zastaralé, vyřazené |
| **TLS 1.2** | stále běžné |
| **TLS 1.3** | aktuální, rychlejší a bezpečnější |

### SSL vs. TLS

SSL je **starý název** – dnes se všude používá TLS, ale hovorově se pořád říká "SSL certifikát". Technicky správně je TLS.

### STARTTLS

Způsob, jak upgradovat už navázané nešifrované spojení na šifrované (běžné u [[SMTP]] na portu 587). Nejde o jiný protokol, jen o příkaz "od teď šifrujeme".

### Certifikát a důvěra

Server pošle certifikát podepsaný **certifikační autoritou (CA)**. Prohlížeč a systém mají seznam důvěryhodných CA. Když podpis sedí a jméno v certifikátu odpovídá adrese webu, spojení je ověřené. Jinak prohlížeč varuje.

### TLS 1.3 vs. 1.2

| | TLS 1.2 | TLS 1.3 |
| :-- | :-- | :-- |
| handshake | 2 výměny tam a zpět | 1 výměna (rychlejší) |
| staré slabé šifry | ještě povolené | odstraněné |
| výměna klíčů | i bez forward secrecy | vždy s forward secrecy |

**Forward secrecy** = i kdyby později unikl soukromý klíč serveru, staré nahrané relace nejdou rozšifrovat.

### TLS a další protokoly

TLS nepoužívá jen web: [[HTTPS]] (443), IMAPS (993), SMTP se STARTTLS, LDAPS, VPN (některé typy).

**Souvisí:** [[HTTPS]], [[HTTP]], [[SMTP]], [[IMAP]], [[POP3]], [[FTP]], [[TCP]]
