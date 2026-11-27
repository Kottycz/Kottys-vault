---
aliases: [User Datagram Protocol]
tags: [slovnik]
---

# UDP

**User Datagram Protocol** – nespolehlivý, nespojovaný protokol transportní vrstvy (OSI 4). Data pošle bez navazování spojení a bez potvrzování – je rychlý, ale nezaručuje doručení.

---

## Podrobně

### Co řeší

UDP je minimalistický protokol. Nepřidává skoro nic k tomu, co umí IP – jen [[port|porty]] (aby se data dostala správné aplikaci) a kontrolní součet. Všechno ostatní (spolehlivost, pořadí) musí případně zajistit sama aplikace.

### Vlastnosti

- **Nespojovaný (connectionless)** – žádný handshake, odesílá se rovnou.
- **Bez potvrzování** – odesílatel se nikdy nedozví, jestli data dorazila.
- **Nezaručuje pořadí** – datagramy můžou dorazit přeházené.
- **Bez řízení toku a zahlcení** – odesílá plnou rychlostí bez ohledu na stav sítě.

### Hlavička

Pouhých **8 bajtů**:

| Pole | Velikost |
| :-- | :-- |
| Zdrojový port | 2 B |
| Cílový port | 2 B |
| Délka | 2 B |
| Checksum | 2 B |

Pro srovnání [[TCP]] má hlavičku 20 B – UDP tedy plýtvá méně kapacity na režii.

### PDU

Jednotka dat UDP se nazývá **datagram** (viz [[PDU]]).

### Kde se používá

Tam, kde je rychlost důležitější než dokonalost:

- **Streaming** (video, audio) – ztracený paket se nevyplatí posílat znovu, obraz by se zasekl
- **Online hry** – nízká [[latency|latence]] je klíčová
- **VoIP** – telefonie přes internet
- **[[DNS]]** – krátký dotaz a odpověď, opakování je levnější než handshake
- **[[DHCP]]**, TFTP, SNMP

### Proč nespolehlivost nevadí

U streamu je lepší přeskočit jeden vzorek zvuku než čekat na jeho doručení a zaseknout přehrávání. Pokud aplikace přece jen potřebuje spolehlivost, může si ji dodělat sama nad UDP (dělá to např. QUIC/HTTP/3).

### Porty známých UDP služeb

| Služba | Port |
| :-- | :-- |
| [[DNS]] | 53 |
| [[DHCP]] | 67 (server), 68 (klient) |
| [[TFTP]] | 69 |
| SNMP | 161, 162 |
| Syslog | 514 |
| NTP | 123 |

### Kdo hlídá spolehlivost

UDP nic nepotvrzuje. Když aplikace spolehlivost potřebuje, musí si ji zajistit sama: [[TFTP]] potvrzuje každý blok, [[DNS]] dotaz po timeoutu pošle znovu. Nový protokol **QUIC** (základ HTTP/3) běží nad UDP a spolehlivost i šifrování řeší sám.

### UDP a firewall

Protože UDP nemá spojení, stavový firewall si pro něj „spojení" vymýšlí: odpověď pustí, když přijde ze správné adresy a portu do krátké doby po odeslání dotazu.

**Souvisí:** [[TCP]], [[port]], [[socket]], [[PDU]], [[latency]]
