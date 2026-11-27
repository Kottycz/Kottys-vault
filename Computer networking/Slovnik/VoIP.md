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

### Kodeky

| Kodek | Přenosová rychlost | Kvalita |
| :-- | :-- | :-- |
| G.711 | 64 kb/s | jako klasický telefon, bez komprese |
| G.729 | 8 kb/s | komprese, šetří linku |
| Opus | proměnná | moderní, používají ho aplikace (Teams, WhatsApp) |

K samotnému kodeku se přidají hlavičky IP/UDP/RTP, takže hovor G.711 zabere na lince kolem 80–90 kb/s v každém směru.

### Požadavky na síť

Jednosměrné zpoždění do **150 ms**, jitter do **30 ms**, ztráty do **1 %**. Proto se hlas dává do [[Voice VLAN]] a prioritizuje přes [[QoS]].

### Napájení telefonů

IP telefony se napájí přes [[PoE]] ze switche. Při výpadku proudu fungují, jen když má switch záložní napájení (UPS).

**Souvisí:** [[UDP]], [[QoS]], [[DSCP]], [[latency]], [[LAN]]
