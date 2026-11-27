---
aliases: [Border Gateway Protocol]
tags: [slovnik]
---

# BGP

**Border Gateway Protocol** – směrovací protokol, na kterém stojí internet. Vyměňuje si trasy mezi **autonomními systémy** (velkými sítěmi poskytovatelů).

---

## Podrobně

### Autonomní systém (AS)

Síť pod jednou správou s vlastním číslem (ASN) – typicky poskytovatel internetu, velká firma nebo Google. BGP řeší, jak se mezi těmito systémy dostane provoz.

### Interior vs. exterior

| Typ | Kde | Protokoly |
| :-- | :-- | :-- |
| **IGP** (interior) | uvnitř jednoho AS | [[OSPF]], EIGRP, RIP |
| **EGP** (exterior) | mezi AS | **BGP** |

[[OSPF]] řeší směrování uvnitř firmy, BGP mezi poskytovateli.

### Čím se liší od OSPF

| | [[OSPF]] | BGP |
| :-- | :-- | :-- |
| Typ | link-state | **path vector** |
| Metrika | šířka pásma (cost) | politiky, délka cesty přes AS |
| Konvergence | vteřiny | minuty |
| Velikost tabulky | desítky tras | **1 milion+** tras |
| Transport | vlastní | nad [[TCP]] (port 179) |

BGP nevybírá nejrychlejší cestu, ale cestu podle **obchodních pravidel** – kdo komu platí za tranzit.

### Proč je křehký

BGP je postavený na důvěře – když někdo omylem (nebo schválně) inzeruje cizí adresní rozsah, provoz se k němu začne směrovat. Tak vznikají velké výpadky:

- 2008: Pákistán omylem "ukradl" YouTube pro celý svět
- 2021: výpadek Facebooku – jeho BGP trasy zmizely z internetu

Obrana: **RPKI** (kryptografické ověření, kdo smí inzerovat který rozsah).

### Technické vlastnosti

- běží nad [[TCP]] na portu **179** (sousedé si spojení navazují ručně nakonfigurovaní, ne automaticky),
- typ **path vector** – u každé cesty si pamatuje seznam AS, přes které vede (**AS_PATH**). Když v cestě vidí svoje AS číslo, cestu zahodí → nevzniknou smyčky,
- nevybírá nejrychlejší cestu, ale podle **politik** (smlouvy a ceny mezi poskytovateli).

### eBGP vs. iBGP

| | eBGP | iBGP |
| :-- | :-- | :-- |
| mezi | různými AS | routery uvnitř stejného AS |
| [[router|AD]] | 20 | 200 |

### Kdo ho používá

[[ISP|Poskytovatelé internetu]], velké firmy připojené k víc ISP najednou, cloudy. V malé firmě nebo škole se nepoužívá, tam stačí výchozí cesta k ISP.

**Souvisí:** [[OSPF]], [[router]], [[TCP]], [[IP adresa]], [[WAN]]
