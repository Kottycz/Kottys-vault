# Inter-VLAN Routing #1

CCNA 2 (SRWE), modul 4, část 1. Navazuje na [[VLAN_cast_1]] a [[VLAN_cast_2]]. Viz [[VLAN]], [[Inter-VLAN routing]].

Hostitelé mohou komunikovat s ostatními hostiteli ve stejné síti [[VLAN]] a hostitelé již nemusí odesílat zprávy [[broadcast|všesměrového vysílání]] všem ostatním zařízením ve vaší síti, což spotřebovává potřebnou [[šířka pásma|šířku pásma]]. Co když ale hostitel v jedné síti VLAN potřebuje komunikovat s hostitelem v jiné síti VLAN? Pokud jste správce sítě, víte, že lidé budou chtít komunikovat s dalšími lidmi mimo vaši síť. Zde vám může pomoci [[Inter-VLAN routing|směrování mezi sítěmi VLAN]]. Směrování mezi sítěmi VLAN využívá zařízení [[Sitova_vrstva|vrstvy 3]], jako je [[router]] nebo [[přepínač vrstvy 3]].

Hostitelé v jedné síti VLAN komunikovat s hostiteli v jiné síti VLAN nemohou, pokud není k dispozici router nebo přepínač vrstvy 3, který poskytuje směrovací služby.

## Možnosti směrování mezi VLAN

1. tradiční (legacy) směrování mezi VLAN
2. [[Router-on-a-Stick]]
3. Přepínač vrstvy 3 využívající přepínaná virtuální rozhraní ([[SVI]])

## ad 2) Router-on-a-Stick

Pro směrování provozu mezi více VLAN v síti vyžaduje pouze jedno fyzické [[Ethernet|ethernetové]] rozhraní. Ethernetové rozhraní routeru Cisco [[IOS]] je konfigurováno jako trunk [[802.1Q]] a připojeno k portu [[VLAN trunk|trunku]] na přepínači Layer 2 (software-based virtual sub-interfaces). Každý [[subinterface|sub-interface]] je nezávisle konfigurován s [[IP adresa|IP adresou]] a přiřazením k VLAN. Když „tagovaný" rámec VLAN vstoupí do rozhraní routeru, přijme ho podrozhraní zdrojové VLAN podle tagu. Router paket směruje podle cílové IP adresy a odešle ho přes podrozhraní cílové VLAN s novým tagem.

Př. pro Router R1 Subinterfaces:

| Subinterface | VLAN | IP Address |
| :-- | :-- | :-- |
| G0/0/1.10 | 10 | 192.168.10.1/24 |
| G0/0/1.20 | 20 | 192.168.20.1/24 |
| G0/0/1.99 | 99 | 192.168.99.1/24 |

[[Rozhrani_routeru_dual_stack|Konfigurační příkazy]] (pro každý sub-interface):

```
interface interface-id.subinterface-id
encapsulation dot1q vlan_id [native]
ip address ip-address subnet-mask
```

Aktivace fyzického rozhraní (stačí jednou):

```
interface interface-id
no shutdown
```

[[Overovani_primo_pripojenych_siti|Verifikační příkazy]]: `show ip route`, `show ip interface brief`, `show interfaces`, `show interfaces trunk`

## Z hodiny – tabule

![[inter-vlan-tabule.png]]

### Vlevo: Router-on-a-Stick

- nahoře **[[router]] R**, šipka nahoru = cesta ven do dalších sítí,
- na jednom fyzickém rozhraní routeru jsou tři **[[subinterface|podrozhraní]]** (SUB-IF) pro VLAN1, VLAN2 a VLAN3,
- z R vede **[[VLAN trunk|trunk]] (T)** do switche S1, z S1 další trunk do S2,
- na S1: PC1 (zakroužkované) ve VLAN1, další porty ve VLAN1 a VLAN2,
- na S2: dvě PC ve VLAN1, jedno PC (zakroužkované) ve VLAN2.

**Nakreslená cesta** z PC1 (VLAN1, na S1) do zakroužkovaného PC ve VLAN2 na S2:

```
PC1 → S1 → trunk nahoru → R (přijde na podrozhraní VLAN1)
  → R přesměruje na podrozhraní VLAN2
  → stejný trunk dolů → S1 → trunk → S2 → PC ve VLAN2
```

Pointa: provoz mezi dvěma VLAN musí **až na router a zpátky po stejném kabelu**, i když jsou obě PC fyzicky kousek od sebe. Proto je trunk k routeru úzké hrdlo.

### Vpravo: přepínač vrstvy 3 (S-L3)

- jeden [[přepínač vrstvy 3|switch]], který umí L3 (směrování) i L2 (přepínání) – proto na tabuli „S-L3 (L2)",
- uvnitř má rozhraní pro VLAN1 a VLAN2 ([[SVI]]),
- porty dole jsou rozdělené do VLAN1 (PC1) a VLAN2 (PC2),
- provoz mezi VLAN se přesměruje **přímo uvnitř switche**, nikam ven na router nejde.

> [!warning] Nejisté
> Pravá část byla na tabuli nedokreslená. Jisté je: nadpis „S-L3 (L2)", box S-L3, porty dole rozdělené na VLAN1 (PC1) a VLAN2 (PC2) a nad boxem čárami vyvedené popisky VLAN (podobně jako podrozhraní u routeru). Že jde o **SVI**, je výklad podle učiva, na tabuli to slovo nebylo. Význam „(L2)" a jeden popisek vlevo od boxu nejsou jisté – ověřit u učitele.

**Souvisí:** [[Inter-VLAN routing]], [[Router-on-a-Stick]], [[subinterface]], [[přepínač vrstvy 3]], [[SVI]], [[VLAN]], [[VLAN trunk]], [[802.1Q]], [[nativní VLAN]], [[router]], [[směrovací tabulka]], [[příkazy show]], [[default gateway]], [[Sprava_switche_SVI]]

**Předchozí:** [[VLAN_cast_2]]
