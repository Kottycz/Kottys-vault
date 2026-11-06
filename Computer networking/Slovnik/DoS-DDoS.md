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

**Souvisí:** [[firewall]], [[SPI]], [[MITM]]
