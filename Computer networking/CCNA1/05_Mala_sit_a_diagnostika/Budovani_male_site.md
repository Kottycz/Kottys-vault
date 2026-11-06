# Budování malé sítě

Většina podniků je malých, proto není divu, že i většina obchodních sítí je malých rozměrů.

- Návrh malé sítě je obvykle **jednoduchý**.
- Počet a typ zahrnutých zařízení je ve srovnání s větší sítí výrazně menší.
- Správa malé sítě vyžaduje mnoho **stejných dovedností** jako správa větší sítě.
- Malé sítě spravuje **místní IT technik** nebo **smluvní profesionál**.

## Výběr zařízení pro malou síť

Stejně jako velké sítě, i malé sítě vyžadují **plánování a návrh** tak, aby splňovaly požadavky uživatelů.

| Hledisko | Co to znamená |
| :-- | :-- |
| **Náklady** | Cena [[switch\|přepínače]] nebo [[router\|routeru]] je určena jeho kapacitou a funkcemi. To zahrnuje počet a typy dostupných portů a rychlost propojovací desky. |
| **Rychlost a typy portů/rozhraní** | I když je to dražší, výběr zařízení vrstvy 2, která zvládnou vyšší rychlosti, umožňuje síť vyvíjet se **bez nutnosti výměny centrálních zařízení**. |
| **Rozšiřitelnost** | Síťová zařízení jsou k dispozici v **pevné** a **modulární** fyzické konfiguraci. Zařízení s pevnou konfigurací mají specifický počet a typ portů nebo rozhraní a nelze je rozšiřovat – viz [[modulární zařízení]]. |
| **Funkce a služby operačního systému** | Zařízení nabízejí různé funkce a služby operačního systému (u Cisco viz [[IOS]]). |

## IP adresování

- Při implementaci sítě vytvořte **schéma IP adresování** a používejte ho – viz [[schéma IP adresování]].
- Všichni hostitelé a zařízení v rámci sítě musí mít **jedinečnou adresu** ([[IP adresa]]).
- Plánované schéma usnadňuje **identifikaci typu zařízení** a **řešení problémů**, například při řešení problémů se síťovým provozem pomocí [[sniffer|analyzátoru protokolů]].

## Redundance v malé síti

- Další důležitou součástí návrhu sítě je **spolehlivost**.
- Pro zachování vysokého stupně spolehlivosti je v návrhu sítě nutná [[redundance]].
- Redundance pomáhá eliminovat **jednotlivé body selhání** ([[single point of failure]]).

## Růst malé sítě

Pokud je síť určena pro malou firmu, pravděpodobně chceš, aby firma rostla a s ní rostla i síť. Tomu se říká [[škálování sítě]] a existuje několik osvědčených postupů, jak toho dosáhnout.

Pro škálování sítě je zapotřebí několik prvků:

- **Dokumentace sítě**
- **Inventář zařízení**
- **Rozpočet**
- **Analýza provozu**

## Ověření připojení

### ping

[[ping|Příkaz ping]] je **nejúčinnější způsob**, jak rychle otestovat konektivitu **vrstvy 3** mezi zdrojovou a cílovou IP adresou.

- Používá zprávy [[echo request]] (**ICMP typ 8**) a echo reply (**ICMP typ 0**) protokolu [[ICMP]] (Internet Control Message Protocol).
- Je užitečný pro rychlé zjištění, zda se jedná o problém s připojením na vrstvě 3.
- **Neidentifikuje však, kde se problém podél cesty nachází.**

### Rozšířený ping

Systém Cisco IOS nabízí „rozšířený" režim příkazu ping. Tento režim umožňuje vytvářet speciální typy příkazů ping **úpravou parametrů** souvisejících s operací příkazu. Viz [[rozšířený ping]].

### traceroute

[[traceroute|Traceroute]] může pomoci **lokalizovat problémové oblasti** na 3. vrstvě v síti.

- Trace vrací **seznam uzlů ([[hop|hopů]])** při směrování paketu sítí.
- Lze jej použít k identifikaci **bodu na cestě, kde se problém nachází**.

| Nástroj | Odpovídá na |
| :-- | :-- |
| **ping** | Je problém s připojením na vrstvě 3? |
| **traceroute** | Kde se na cestě problém nachází? |

## Diagnostické příkazy

### Příkazy na hostiteli

[[ipconfig]]:

```
ipconfig /all
ipconfig /release
ipconfig /renew
arp -a
```

- `ipconfig /all` – kompletní nastavení síťových rozhraní
- `ipconfig /release` a `ipconfig /renew` – uvolnění a obnovení adresy od [[DHCP]]
- `arp -a` – zobrazení [[ARP]] tabulky

### Příkazy IOS – show

[[příkazy show|show]]:

```
show running-config
show interfaces
show ip interface
show ip interface brief
show arp
show ip route
show protocols
show version
```

| Příkaz | Co ukáže |
| :-- | :-- |
| `show running-config` | aktuální konfiguraci ([[running-config]]) |
| `show interfaces` | stav a statistiky rozhraní |
| `show ip interface` (`brief`) | IP nastavení rozhraní (`brief` = zkrácený přehled) |
| `show arp` | [[ARP]] tabulku |
| `show ip route` | směrovací tabulku |
| `show protocols` | zapnuté protokoly |
| `show version` | verzi a údaje o zařízení |

### Příkaz zobrazit sousedy – CDP

Existuje několik dalších užitečných příkazů pro IOS. [[CDP]] (Cisco Discovery Protocol) je **proprietární protokol** společnosti Cisco, který běží na **vrstvě datového spojení**.

- Protože CDP pracuje na vrstvě datového spojení, dvě nebo více síťových zařízení Cisco (například [[router|směrovače]]), která podporují různé protokoly síťové vrstvy, se o sobě mohou dozvědět, **i když nebylo navázáno připojení na 3. vrstvě**.

```
show cdp neighbor
```

CDP se zakazuje:

- **globálně** – příkaz globální konfigurace `no cdp run`
- **na rozhraní** – příkaz rozhraní `no cdp enable`

### Příkaz ladění – debug

**Procesy, protokoly, mechanismy a události** operačního systému generují **zprávy**, které sdělují jejich stav. Tyto zprávy mohou poskytnout cenné informace při řešení problémů nebo ověřování systémových operací.

- Příkaz IOS [[debug]] umožňuje administrátorovi zobrazit tyto zprávy **v reálném čase** pro účely analýzy.
- Je to velmi důležitý nástroj pro monitorování událostí na zařízení Cisco IOS.

```
debug ip icmp
debug ?
```

- `debug ip icmp` – sledování stavu zpráv [[ICMP]] v routeru Cisco
- `debug ?` – stručný popis všech možností ladicího příkazu

Některé zprávy systému IOS se automaticky zobrazují při připojení ke konzoli, **ale ne při vzdáleném připojení**. Například ladicí výstup se ve výchozím nastavení zobrazuje při připojení ke konzoli. Při vzdáleném připojení se výstup zapíná příkazem:

```
terminal monitor
```

Viz [[terminal monitor]].

**Souvisí:** [[ping]], [[traceroute]], [[ICMP]], [[IOS]], [[CDP]], [[škálování sítě]], [[redundance]], [[Zakladni_konfigurace_zarizeni]]
