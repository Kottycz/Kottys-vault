---
aliases: [Spanning Tree Protocol, STP protokol]
tags: [slovnik]
---

# STP protokol

**Spanning Tree Protocol** – protokol, který brání vzniku **smyček** na [[switch|switchích]]. Nadbytečné cesty logicky zablokuje a nechá jen jednu aktivní.

---

## Podrobně

### Proč je potřeba

Když se switche propojí do kruhu (kvůli záloze), [[broadcast]] začne kolovat donekonečna:

```
Switch A ──── Switch B
    │             │
    └─ Switch C ──┘

Broadcast obíhá pořád dokola → broadcast storm → síť zamrzne
```

Na rozdíl od [[IP adresa|IP paketů]] nemají rámce [[TTL]], takže je nic nezastaví. To je zásadní problém – síť se zahltí během vteřin.

### Jak funguje

1. Switche si zvolí **root bridge** (kořenový switch, ten s nejnižším ID)
2. Každý switch si spočítá nejlevnější cestu ke kořenu
3. Porty, které by tvořily smyčku, se **zablokují** (blocking state)
4. Když aktivní cesta vypadne, záložní port se odblokuje

Výsledkem je stromová struktura bez smyček – proto "spanning tree".

### Verze

| Verze | Popis |
| :-- | :-- |
| **STP** (802.1D) | původní, konvergence ~30–50 s |
| **RSTP** (802.1w) | rapid – konvergence do několika sekund |
| **MSTP** (802.1s) | vlastní strom pro každou skupinu [[VLAN]] |

### PortFast

Na portech ke koncovým zařízením se zapíná **PortFast** – port přejde rovnou do provozu a nečeká na STP. Bez toho trvá desítky sekund, než počítač po zapojení dostane adresu z [[DHCP]].

### Pozor na zkratku

**STP** má v sítích dva významy:
- **STP protokol** = Spanning Tree Protocol (tohle)
- **[[STP kabel]]** = Shielded Twisted Pair (stíněný kabel)

### Volba root bridge

1. každý switch má **Bridge ID** = priorita (výchozí **32768**) + VLAN + [[MAC adresa]],
2. **nejnižší Bridge ID** vyhraje a stane se root bridge,
3. při stejné prioritě rozhodne nejnižší MAC (často nejstarší switch, což není ideální).

Root bridge se proto nastavuje ručně:

```
S1(config)# spanning-tree vlan 1 root primary
S1(config)# spanning-tree vlan 1 priority 4096
```

### Role portů

| Role | Význam |
| :-- | :-- |
| root port | na každém switchi (kromě root) port s nejlevnější cestou k root bridge |
| designated port | na každém segmentu port, který přeposílá směrem od rootu |
| alternate / blocked | záložní port, blokuje, aby nevznikla smyčka |

### Stavy portu (klasický STP)

Blocking → Listening (15 s) → Learning (15 s) → Forwarding. Proto trvá klasickému STP naběhnutí portu kolem **30–50 s**. RSTP to zvládne za pár sekund.

### BPDU Guard

Na portech s PortFast se zapíná **BPDU Guard**: když na port přijde BPDU (někdo připojil switch), port se vypne (err-disabled). Chrání před smyčkou z nechtěně připojeného switche.

### Ověření

`show spanning-tree` – kdo je root, role a stav portů.

**Souvisí:** [[switch]], [[broadcast]], [[VLAN]], [[STP kabel]]
