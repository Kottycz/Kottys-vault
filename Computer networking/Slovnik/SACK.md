---
aliases: [Selective Acknowledgment, selektivní potvrzování]
tags: [slovnik]
---

# SACK

**Selective Acknowledgment** – rozšíření [[TCP]], které umožňuje potvrdit i segmenty přijaté **mimo pořadí**. Díky tomu se po ztrátě neposílá znovu všechno, ale jen to, co chybí.

---

## Podrobně

### Problém bez SACK

Klasické TCP potvrzuje jen souvislý úsek – "mám všechno do pozice X":

```
Odesláno:  1  2  3  4  5
Přijato:   1  2  ✗  4  5      (3 se ztratil)

Bez SACK:  příjemce potvrdí jen "mám do 2"
           → odesílatel pošle znovu 3, 4, 5  ← zbytečně
```

### S SACK

```
S SACK:    "mám do 2, a navíc mám 4 a 5"
           → odesílatel pošle znovu jen 3   ← efektivní
```

Ušetří se tím kapacita i čas, hlavně na linkách s vysokou [[latency|latencí]].

### Dva režimy příjemce

| Režim | Chování |
| :-- | :-- |
| **in-order** | přijímá jen data v pořadí, ostatní zahazuje (jednodušší, méně efektivní) |
| **out-of-order** | ukládá i data mimo pořadí a potvrzuje je přes SACK |

### Jak se zapne

SACK se domlouvá při [[3-way handshake]] – obě strany musí souhlasit. Dnes ho podporují prakticky všechny systémy a je zapnutý ve výchozím stavu.

**Souvisí:** [[TCP]], [[sliding window]], [[3-way handshake]], [[latency]]
