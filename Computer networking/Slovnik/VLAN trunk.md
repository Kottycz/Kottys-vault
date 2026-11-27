---
aliases: [trunk, trunk port, kmenová linka, VLAN Trunks]
tags: [slovnik]
---

# VLAN trunk

**VLAN trunk** – spoj mezi přepínači, kterým se šíří provoz **všech** [[VLAN]] najednou. Příklad: PC ve VLAN 10 na switchi A mluví s PC ve VLAN 10 na switchi B přes trunk, bez routeru.

---

## Podrobně

### Access port vs. trunk port

| | Access port | Trunk port |
| :-- | :-- | :-- |
| kolik VLAN | jednu | víc (výchozí všechny) |
| kam vede | ke koncovému zařízení (PC, tiskárna) | na jiný switch nebo [[router]] |
| tagování | rámce bez tagu | rámce s tagem [[802.1Q]] |
| příkaz | `switchport mode access` | `switchport mode trunk` |

Koncové zařízení o VLAN vůbec neví. Tag přidá switch, až když rámec posílá přes trunk, a druhý switch ho před odesláním na access port zase odebere.

### Proč je trunk potřeba

Bez trunku by každá VLAN mezi dvěma switchi potřebovala vlastní kabel a vlastní port (3 VLAN = 3 kabely). Trunk to zvládne jedním kabelem. Zařízení ve stejné VLAN na různých switchích pak spolu komunikují bez [[router|routeru]].

### Tag 802.1Q

Přes trunk se rámce označují 4bajtovým tagem podle [[802.1Q]], vloženým mezi zdrojovou MAC a [[EtherType]]:

| Část tagu | Velikost | K čemu |
| :-- | :-- | :-- |
| TPID | 16 b | hodnota `0x8100` = „tohle je tagovaný rámec" |
| PCP | 3 b | priorita rámce ([[QoS]], např. pro hlas) |
| DEI | 1 b | rámec lze při přetížení zahodit |
| VID | 12 b | číslo VLAN (1–4094) |

Protože se rámec změní, switch musí přepočítat [[FCS]].

### Nativní VLAN na trunku

- rámce [[nativní VLAN]] jdou přes trunk **bez tagu**,
- výchozí nativní VLAN je **VLAN 1**,
- **na obou koncích trunku musí být stejná**. Když se liší, provoz se míchá mezi VLAN a [[CDP]] hlásí chybu „native VLAN mismatch".

### Konfigurace

```
S1(config)# interface g0/1
S1(config-if)# switchport mode trunk
S1(config-if)# switchport trunk native vlan 99
S1(config-if)# switchport trunk allowed vlan 10,20,30,99
S1(config-if)# end
```

- `allowed vlan` – omezí, které VLAN smí přes trunk (jinak jdou všechny),
- `allowed vlan add 40` – přidá VLAN do seznamu, bez `add` se celý seznam přepíše,
- zrušení: `no switchport trunk allowed vlan`, `no switchport trunk native vlan`.

### Ověření

```
S1# show interfaces trunk
S1# show interfaces g0/1 switchport
```

`show interfaces trunk` ukáže, které porty jsou trunk, jejich nativní VLAN, povolené VLAN a VLAN, které jsou na trunku skutečně aktivní.

### Vyjednání trunku – DTP

Cisco switche umí trunk dohodnout samy přes [[DTP]] (`dynamic auto`, `dynamic desirable`). Spolehlivější a bezpečnější je nastavit trunk ručně (`switchport mode trunk`) a vyjednávání vypnout (`switchport nonegotiate`).

### Bezpečnost

- nativní VLAN změnit z VLAN 1 na **nepoužívanou VLAN** (chrání proti útoku VLAN hopping s dvojitým tagem),
- povolit na trunku **jen potřebné VLAN**,
- vypnout DTP, aby útočník nemohl ze svého PC vyjednat trunk a vidět všechny VLAN,
- nepoužívané porty dát do nepoužívané VLAN a vypnout (`shutdown`).

### Trunk na router

Trunk nevede jen mezi switchi. U [[Router-on-a-Stick]] vede trunk ze switche na jedno rozhraní routeru a router má pro každou VLAN [[subinterface]].

**Souvisí:** [[VLAN]], [[802.1Q]], [[nativní VLAN]], [[DTP]], [[switch]], [[router]], [[Router-on-a-Stick]], [[VLAN_cast_2]]
