---
aliases: [Internet Service Provider, poskytovatel internetu]
tags: [slovnik]
---

# ISP

**Internet Service Provider** – poskytovatel připojení k internetu. Propojuje zákazníkovu [[LAN]] se zbytkem internetu přes svou [[WAN]] síť.

---

## Podrobně

### Co zákazníkovi poskytuje

- Fyzické připojení (optika, DSL, kabel, mobilní síť)
- **Veřejnou [[IP adresa|IP adresu]]** (obvykle jednu, proto se doma používá [[NAT]])
- [[DNS]] servery
- Případně zařízení (modem, [[router]] – označuje se CPE)

### Úrovně poskytovatelů

| Tier | Popis |
| :-- | :-- |
| **Tier 1** | páteřní sítě, propojené navzájem zdarma (peering), za tranzit neplatí nikomu |
| **Tier 2** | regionální, kupují tranzit od Tier 1 |
| **Tier 3** | lokální, prodávají koncovým zákazníkům |

Mezi sebou si trasy vyměňují protokolem [[BGP]].

### Peering a NIX

Poskytovatelé si vyměňují provoz v propojovacích uzlech – v ČR je to **NIX.CZ**. Díky tomu nemusí provoz mezi dvěma českými sítěmi cestovat přes zahraničí, což šetří peníze i [[latency|latenci]].

### Pojmy u připojení

| Pojem | Význam |
| :-- | :-- |
| **CPE** | zařízení u zákazníka (modem, router) |
| **Poslední míle** | úsek od sítě poskytovatele k zákazníkovi |
| **Agregace** | kolik zákazníků sdílí jednu kapacitu (1:20 = rychlost není garantovaná) |
| **Symetrie** | stejná rychlost nahoru i dolů (u optiky ano, u DSL ne) |

### Typy připojení

| Typ | Médium | Poznámka |
| :-- | :-- | :-- |
| [[DSL]] | telefonní linka | asymetrické, závisí na vzdálenosti |
| kabelové | koaxiál kabelové TV | sdílené mezi sousedy |
| optika (FTTH) | [[optické vlákno]] až domů | nejrychlejší |
| bezdrátové / mobilní | rádiové vlny, 4G/5G | dostupné všude |
| satelitní | satelit | velká [[latency|latence]] (u geostacionárních) |

### Co ISP přidělí

- veřejnou IP adresu (nebo jen adresu za jeho [[NAT]]em, tzv. CGNAT),
- adresy [[DNS]] serverů,
- u IPv6 celý prefix (např. `/56` nebo `/48`) pro tvoje podsítě.

### Redundance

Firma, která nesmí přijít o internet, má linky od **dvou různých ISP**. Výpadek jednoho poskytovatele ji neodřízne.

**Souvisí:** [[WAN]], [[LAN]], [[BGP]], [[NAT]], [[IP adresa]], [[router]]
