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

### Jam signál a backoff

1. když vysílající zjistí kolizi, pošle **jam signál** (32 bitů), aby kolizi zaznamenali všichni,
2. pak každý počká **náhodnou dobu** (backoff) a zkusí to znovu,
3. při každé další kolizi se rozsah náhodného čekání zdvojnásobí (**binary exponential backoff**),
4. po **16** neúspěšných pokusech se rámec zahodí.

### Proč minimální rámec 64 bajtů

Vysílající musí kolizi zjistit, **dokud ještě vysílá**. Doba, kterou signál potřebuje na cestu tam a zpátky přes celou síť, se nazývá **slot time** = 512 bitů. Rámec proto musí mít aspoň 512 bitů = **64 bajtů**. Kratší rámce jsou [[runt|runty]] a zahazují se. Kolize po prvních 64 bajtech je [[late collision]] a značí chybu.

**Souvisí:** [[CSMA-CA]], [[switch]], [[full-duplex]], [[half-duplex]]
