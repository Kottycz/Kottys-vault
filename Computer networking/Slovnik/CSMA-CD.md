---
aliases: [CSMA/CD, Carrier Sense Multiple Access with Collision Detection]
tags: [slovnik]
---

# CSMA-CD

**Carrier Sense Multiple Access with Collision Detection** – přístupová metoda klasického Ethernetu. Zařízení poslouchá linku, a když zjistí kolizi, přenos přeruší a zkusí to znovu.

---

## Podrobně

### Postup

```
1. Carrier Sense     – poslouchej, jestli je linka volná
2. Multiple Access   – je-li volná, vysílej
3. Collision Detect  – během vysílání kontroluj kolizi
4. Při kolizi:
   - pošli jam signál (ať to vědí všichni)
   - počkej náhodnou dobu (backoff)
   - zkus to znovu
```

Náhodná doba čekání je klíčová – kdyby všichni čekali stejně dlouho, kolize by se opakovala donekonečna.

### Kdy vzniká kolize

Když dvě zařízení vysílají zároveň po sdíleném médiu – signály se přeruší a data jsou znehodnocená.

### Proč se dnes nepoužívá

CSMA/CD dávalo smysl u **hubů a koaxiálních kabelů**, kde všichni sdíleli jedno médium. Dnešní [[switch|switche]] s [[full-duplex]] provozem kolize **fyzicky vylučují** – každý port má vlastní kolizní doménu a data tečou oběma směry současně po oddělených párech.

CSMA/CD je tedy dnes už jen **historie**, stále se ale učí, protože vysvětluje, proč switche nahradily huby.

### CSMA/CD vs. CSMA/CA

| | CSMA/CD | [[CSMA-CA]] |
| :-- | :-- | :-- |
| Prostředí | drátový Ethernet | Wi-Fi |
| Přístup | detekuje kolizi *po* vzniku | snaží se jí *předejít* |
| Proč jinak | na drátě lze kolizi slyšet | v rádiu nelze vysílat a poslouchat zároveň |

**Souvisí:** [[CSMA-CA]], [[switch]], [[full-duplex]], [[half-duplex]]
