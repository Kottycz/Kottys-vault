---
aliases: [Voice over IP, internetová telefonie]
tags: [slovnik]
---

# VoIP

**Voice over IP** – přenos hlasových hovorů přes datovou síť místo klasické telefonní linky. Základ konvergovaných sítí.

---

## Podrobně

### Jak funguje

1. Mikrofon zaznamená zvuk
2. **Kodek** ho převede na digitální data a zkomprimuje (G.711, G.729, Opus)
3. Data se rozdělí do malých paketů a pošlou přes [[UDP]]
4. Na druhé straně se složí zpět na zvuk

### Proč UDP a ne TCP

Ztracený vzorek zvuku nemá smysl posílat znovu – než by dorazil, hovor by už byl někde jinde. Lepší je přeskočit malý kousek než zaseknout celý hovor. Proto VoIP jede nad [[UDP]] (konkrétně protokolem **RTP**).

### Na čem VoIP závisí

| Parametr | Požadavek |
| :-- | :-- |
| **[[latency]]** | pod ~150 ms (nad tím se lidé začnou překřikovat) |
| **Jitter** | co nejmenší kolísání |
| **Ztrátovost** | pod 1 % |
| **[[šířka pásma]]** | malá (~64–100 kb/s na hovor) |

VoIP tedy nepotřebuje velkou kapacitu, ale **stabilní** spojení – proto se mu v [[QoS]] dává nejvyšší priorita (značka **EF** v poli [[DSCP]]).

### Protokoly

| Protokol | K čemu |
| :-- | :-- |
| **SIP** | navázání, ukončení a správa hovoru |
| **RTP** | samotný přenos zvuku (nad [[UDP]]) |
| **RTCP** | statistiky o kvalitě hovoru |

### Konvergovaná síť

Dřív měla firma zvlášť telefonní a zvlášť datovou síť. Dnes jede hlas, video i data po **jedné infrastruktuře** – levnější na provoz, ale vyžaduje dobře nastavené QoS.

**Souvisí:** [[UDP]], [[QoS]], [[DSCP]], [[latency]], [[LAN]]
