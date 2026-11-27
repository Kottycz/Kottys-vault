---
aliases: [Denial of Service, Distributed Denial of Service, DoS, DDoS]
tags: [slovnik]
---

# DoS-DDoS

**Denial of Service** – útok, jehož cílem je znepřístupnit službu legitimním uživatelům. Nejznámější a nejobtížněji eliminovatelná forma útoku.

---

## Podrobně

### Jak funguje

Útočník zahltí cíl (server, síťové zařízení, spojení) provozem nebo požadavky, takže cíl přestane zvládat obsluhovat legitimní uživatele.

### DoS vs. DDoS

| | DoS | DDoS |
| :-- | :-- | :-- |
| Zdroj útoku | jeden | víc koordinovaných zdrojů |
| Síla útoku | omezená | mnohem větší, hůř se blokuje |
| Typický nástroj | jeden počítač | **botnet** (síť napadených počítačů) |

**DDoS** (Distributed DoS) je proto obvykle nebezpečnější – blokovat jednu zdrojovou IP adresu nestačí, útok přichází z tisíců různých míst najednou.

### Obrana

[[firewall|Firewally]] se **stavovou inspekcí paketů** ([[SPI]]) umí rozpoznávat a filtrovat některé typy DoS útoků, plná ochrana proti DDoS ale často vyžaduje specializované služby (scrubbing centra, CDN).

### Typy útoků

| Útok | Jak funguje |
| :-- | :-- |
| SYN flood | spousta SYN bez dokončení [[3-way handshake|handshaku]], server drží polootevřená spojení, dokud mu nedojde paměť |
| ICMP / ping flood | zahlcení [[ping|pingy]] |
| UDP flood | spousta [[UDP]] paketů na náhodné porty |
| amplifikace | útočník pošle malý dotaz (např. [[DNS]]) s podvrženou IP oběti, server pošle oběti mnohem větší odpověď |

### Botnet

DDoS se dělá přes **botnet** – tisíce nakažených zařízení (počítače, kamery, routery), které útočník ovládá na dálku a najednou je pošle útočit na jeden cíl.

### Příznaky

Služba je najednou velmi pomalá nebo nedostupná, linka je plně vytížená, v logu je obrovské množství spojení z mnoha adres.

**Souvisí:** [[firewall]], [[SPI]], [[MITM]]
