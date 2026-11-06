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

**Souvisí:** [[WAN]], [[LAN]], [[BGP]], [[NAT]], [[IP adresa]], [[router]]
