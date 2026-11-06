---
aliases: [HyperText Transfer Protocol]
tags: [slovnik]
---

# HTTP

**HyperText Transfer Protocol** – protokol aplikační vrstvy pro přenos webových stránek. Běží nad [[TCP]] na portu **80**. Nešifrovaný – dnes ho nahrazuje [[HTTPS]].

---

## Podrobně

### Jak funguje

HTTP je **request-response** protokol: klient (prohlížeč) pošle požadavek, server odpoví. Je **bezstavový** – server si mezi požadavky nic nepamatuje (stav se řeší cookies nebo tokeny).

```
Klient                        Server
  |  GET /index.html HTTP/1.1   |
  | --------------------------> |
  |                             |
  |  HTTP/1.1 200 OK            |
  |  <html>...</html>           |
  | <-------------------------- |
```

### Metody (slovesa)

| Metoda | Význam |
| :-- | :-- |
| GET | stáhni zdroj (nemění data) |
| POST | odešli data (např. formulář) |
| PUT | vytvoř/nahraď zdroj |
| DELETE | smaž zdroj |
| HEAD | jako GET, ale jen hlavičky |

### Stavové kódy

| Kód | Skupina | Příklad |
| :-- | :-- | :-- |
| 1xx | informační | 100 Continue |
| 2xx | úspěch | **200 OK** |
| 3xx | přesměrování | 301 Moved Permanently |
| 4xx | chyba klienta | **404 Not Found**, 403 Forbidden |
| 5xx | chyba serveru | **500 Internal Server Error** |

### Verze

- **HTTP/1.1** – dlouho standard, jedno spojení = jeden požadavek po druhém
- **HTTP/2** – multiplexování (víc požadavků najednou po jednom spojení), binární
- **HTTP/3** – běží nad QUIC ([[UDP]]) místo TCP, rychlejší navazování

### Proč se nahrazuje HTTPS

HTTP posílá všechno v čitelné podobě – kdokoliv po cestě (např. na [[switch|switchi]] nebo Wi-Fi) může číst i měnit obsah. Proto se dnes používá [[HTTPS]].

**Souvisí:** [[HTTPS]], [[TCP]], [[port]], [[DNS]]
