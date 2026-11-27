---
aliases: [Stateful Packet Inspection, stavová inspekce paketů]
tags: [slovnik]
---

# SPI

**Stateful Packet Inspection** – schopnost [[firewall|firewallu]] sledovat stav (kontext) spojení, ne jen jednotlivé pakety izolovaně.

---

## Podrobně

### Jak funguje

Příchozí paket musí být legitimní **odpovědí na požadavek** vyslaný z vnitřní sítě. Nevyžádané pakety zvenčí se blokují, pokud nejsou výslovně povolené pravidlem.

```
Vnitřní síť → požadavek ven          → SPI si zapamatuje spojení
Vnější síť  → odpověď na ten požadavek → SPI ji propustí (patří ke spojení)
Vnější síť  → nevyžádaný paket        → SPI ho zablokuje
```

### Stavová vs. bezstavová kontrola

Starší **bezstavové** firewally (jen filtrování paketů podle IP/portu) posuzují každý paket izolovaně. SPI si pamatuje **celý kontext spojení**, takže dokáže odhalit i podvržené pakety, které se tváří jako součást existujícího spojení, ale ve skutečnosti nejsou.

### Detekce útoků

SPI může zahrnovat i schopnost rozpoznávat a filtrovat specifické typy útoků, jako je [[DoS-DDoS|DoS]].

### Tabulka stavů

Stavový firewall si pro každé spojení zapisuje:

| Zdroj | Cíl | Protokol | Stav |
| :-- | :-- | :-- | :-- |
| 192.168.1.5:50123 | 142.250.1.1:443 | TCP | ESTABLISHED |
| 192.168.1.7:53001 | 8.8.8.8:53 | UDP | čeká na odpověď |

Paket zvenku se pustí dovnitř, jen když k němu v tabulce existuje odpovídající záznam (odpověď na vnitřní požadavek).

### Příklad útoku, který SPI zastaví

Útočník pošle zvenku TCP paket s příznakem ACK, jako by šlo o odpověď. Bezstavový filtr by ho pustil („ACK = odpověď"), SPI ho zahodí, protože k němu nepatří žádné navázané spojení.

**Souvisí:** [[firewall]], [[DoS-DDoS]], [[TCP]]
