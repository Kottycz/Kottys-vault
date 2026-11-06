---
aliases: [CSMA/CA, Carrier Sense Multiple Access with Collision Avoidance]
tags: [slovnik]
---

# CSMA-CA

**Carrier Sense Multiple Access with Collision Avoidance** – přístupová metoda Wi-Fi (WLAN). Kolizím se snaží **předejít** dřív, než vzniknou.

---

## Podrobně

### Proč nejde použít CSMA/CD

V rádiovém prostředí zařízení **nemůže zároveň vysílat a poslouchat** – vlastní signál přehluší všechno ostatní. Kolizi tedy nelze během vysílání detekovat, jako to dělá [[CSMA-CD]] na drátě.

### Postup

```
1. Poslouchej, jestli je kanál volný
2. Je-li volný, počkej ještě náhodnou dobu (backoff)
3. Vysílej
4. Čekej na potvrzení (ACK) od příjemce
5. Nepřijde-li ACK → předpokládej kolizi → zkus znovu
```

Potvrzování je tu nutné právě proto, že vysílající o kolizi jinak neví.

### Problém skrytého uzlu

```
  A  ←→  AP  ←→  C
  
A a C na sebe navzájem "nevidí" (jsou daleko),
oba slyší jen přístupový bod (AP).
Oba tedy můžou začít vysílat zároveň → kolize na AP.
```

Řeší se volitelným mechanismem **RTS/CTS**:
- A pošle **RTS** (Request To Send) přístupovému bodu
- AP odpoví **CTS** (Clear To Send), které slyší i C
- C ví, že má mlčet

### Důsledek

Kvůli backoffu, potvrzování a režii je reálná rychlost Wi-Fi výrazně nižší než deklarovaná – a čím víc zařízení na jednom kanálu, tím horší je [[throughput]] pro každého.

**Souvisí:** [[CSMA-CD]], [[half-duplex]], [[throughput]], [[LAN]]
