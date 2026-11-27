---
aliases: [užitečná propustnost]
tags: [slovnik]
---

# goodput

**Užitečná propustnost** – množství **užitečných dat** doručených za jednotku času. Z [[throughput|propustnosti]] odečítá režii protokolů, opakované přenosy a potvrzení.

---

## Podrobně

### Vztah k ostatním pojmům

| Pojem | Hodnota | Co znamená |
| :-- | :-- | :-- |
| [[šířka pásma]] | 1000 Mb/s | teoretické maximum |
| [[throughput]] | 940 Mb/s | co reálně proteče |
| **goodput** | 880 Mb/s | co je z toho použitelné |

### Co se odečítá

| Položka | Příklad |
| :-- | :-- |
| Hlavičky protokolů | Ethernet 18 B + IP 20 B + [[TCP]] 20 B = 58 B režie na rámec |
| Potvrzení ([[ACK]]) | segmenty bez užitečných dat |
| Retransmise | ztracená data poslaná znovu |
| Navazování spojení | [[3-way handshake]], [[TLS]] handshake |

### Příklad

Ethernetový rámec s [[MTU]] 1500 B:

| Položka | Velikost |
| :-- | :-- |
| Rámec (včetně hlaviček a [[FCS]]) | 1518 B |
| − IP hlavička | −20 B |
| − TCP hlavička | −20 B |
| **= užitečná data** ([[MSS]]) | **1460 B** |

Efektivita ≈ 1460 / 1518 ≈ **96 %**

Proto je goodput u velkých souborů vyšší než u mnoha malých paketů – režie se rozloží na víc dat.

### Kdy se to hodí vědět

Když měříš rychlost stahování a nesedí ti to s tím, co slibuje poskytovatel – část kapacity vždy sežere režie.

### Proč je goodput vždy menší

Každá vrstva přidá svou hlavičku. U běžného [[TCP]] segmentu po [[Ethernet|Ethernetu]] s 1460 B dat:

| Režie | Bajty |
| :-- | :-- |
| ethernetová hlavička + FCS | 18 |
| IP hlavička | 20 |
| TCP hlavička | 20 |
| užitečná data | 1460 |

Z 1518 B rámce je užitečných 1460 B, tedy asi 96 %. K tomu se přidá preambule a mezera mezi rámci, potvrzení ([[ACK]]), opakované posílání ztracených segmentů a čekání na handshake. Reálný goodput je proto znatelně nižší.

### Jak ho zlepšit

- méně chyb na lince = méně opakovaného posílání,
- větší rámce (jumbo) = menší podíl hlaviček,
- menší [[latency|latence]] = rychlejší potvrzování.

**Souvisí:** [[throughput]], [[MTU]], [[MSS]], [[latency]], [[TCP]], [[šířka pásma]]
