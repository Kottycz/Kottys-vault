---
tags: [slovnik]
---

# broadcast

**Komunikace jeden na všechny** – data se přenášejí všem zařízením v dané síti (broadcastové doméně).

---

## Podrobně

### Broadcastové adresy

| Vrstva | Adresa |
| :-- | :-- |
| Spojová ([[MAC adresa]]) | `FF:FF:FF:FF:FF:FF` |
| Síťová ([[IPv4]]) – celá síť | `255.255.255.255` |
| Síťová – konkrétní podsíť | všechny host bity = 1, např. `192.168.1.255` |

### Kde se používá

- **[[ARP]] Request** – "kdo má tuhle IP?" (odesílatel nezná cílovou MAC)
- **[[DHCP]] Discover** – klient ještě nemá adresu, tak se ptá všech
- Oznamovací protokoly, objevování zařízení v síti

### Broadcastová doména

Oblast, kam se broadcast dostane:

- **[[switch]]** broadcast **přepošle** na všechny porty → celý switch (VLAN) je jedna broadcastová doména
- **[[router]]** broadcast **zastaví** → router broadcastové domény odděluje

To je hlavní důvod, proč se velké sítě dělí na podsítě – aby broadcast nezatěžoval celou síť.

### Broadcast storm

Když se v síti objeví smyčka (kabel zapojený "do kruhu"), broadcast může kolovat donekonečna a zahltit síť. Brání tomu protokol **STP** (Spanning Tree Protocol), který smyčky logicky přeruší.

### U IPv6

[[IPv6]] **broadcast vůbec nemá**. Nahradil ho cílený [[multicast]] – místo obtěžování všech se zpráva pošle jen relevantní skupině (např. "všechny routery" = `ff02::2`).

### Router a broadcast

- [[router]] **nepřeposílá** broadcasty do jiných sítí, tím ohraničuje [[broadcast doména|broadcast doménu]],
- přeposílání **directed broadcastu** (např. `192.168.1.255` z jiné sítě) je na Cisco routerech ve výchozím stavu vypnuté (`no ip directed-broadcast`). Dřív se toho zneužívalo k útoku Smurf, kdy útočník poslal ping na broadcast adresu cizí sítě a odpovědi zahltily oběť,
- výjimka: `ip helper-address` přepošle [[DHCP]] broadcast na konkrétní server jako unicast.

### Jak broadcasty omezit

- rozdělit síť na menší podsítě nebo [[VLAN]],
- na switchi zapnout **storm-control**, který zahazuje broadcasty nad nastavený limit,
- zabránit smyčkám pomocí [[STP protokol|STP]].

**Souvisí:** [[unicast]], [[multicast]], [[anycast]], [[switch]], [[router]], [[maska podsítě]], [[ARP]], [[DHCP]]
