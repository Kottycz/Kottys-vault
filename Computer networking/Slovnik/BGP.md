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

**Souvisí:** [[OSPF]], [[router]], [[TCP]], [[IP adresa]], [[WAN]]
