# Wireshark – Basics

TryHackMe: **FGP-Wireshark: Basics** (první ze tří místností o Wiresharku). Základy [[Wireshark|Wiresharku]], jak funguje a jak s ním zkoumat zachycený provoz ([[PCAP]]).

## Úvod

| #   | Místnost                                                    | Téma                                   |
| :-- | :---------------------------------------------------------- | :------------------------------------- |
| 1   | **Wireshark Basics**                                        | GUI, disekce paketů, navigace, filtry  |
| 2   | [[02_Wireshark_Packet_Operations\|Packet Operations]]       | statistiky, filtry, operátory, funkce  |
| 3   | [[03_Wireshark_Traffic_Analysis\|Traffic Analysis]]         | hledání útoků a anomálií v provozu     |
| +   | [[04_Wireshark_Video_Mastering\|Video: Mastering Wireshark]] | celkový přehled z videa              |

- **Wireshark** = open-source, multiplatformní nástroj pro **analýzu síťových paketů**
- umí **odposlouchávat živý provoz** a **zkoumat zachycené soubory** ([[PCAP]])
- ve VM jsou dva soubory: `http1.pcapng` (ukázky ze screenshotů) a `Exercise.pcapng` (na otázky)

## Wireshark – přehled

### K čemu se používá

- **řešení problémů v síti** – zatížení, přetížení, místa selhání
- **detekce bezpečnostních anomálií** – podvodní hostitelé, divné využití portů, podezřelý provoz
- **učení se protokolů** – kódy odpovědí, přenášená data

> [!warning] Wireshark **není [[IDS]]**
> - pakety jen **čte**, **nemění** je
> - sám nic nedetekuje – odhalení problému závisí na **znalostech analytika**

### GUI – 5 hlavních částí (úvodní obrazovka)

| Část | Co tam je |
| :-- | :-- |
| **Toolbar** | menu a zkratky pro zachytávání a zpracování (filtrování, třídění, export, slučování) |
| **Display Filter Bar** | hlavní místo pro **dotazy a filtrování** |
| **Recent Files** | nedávno otevřené soubory (dvojklik = otevřít) |
| **Capture Filter and Interfaces** | [[capture filter\|capture filtry]] a dostupná **síťová rozhraní** (`lo`, `eth0`, `ens33`, WLAN…) |
| **Status Bar** | stav nástroje, **profil**, počty paketů |

![[ws_bas_gui_uvod.png|650]]

- **síťové rozhraní** = spojovací bod mezi počítačem a sítí

### Načtení PCAP

- **File → Open**, přetažení souboru, nebo dvojklik na `.pcap`
- po načtení jsou detaily paketů ve **třech panelech**:

| Panel | Co ukazuje |
| :-- | :-- |
| **Packet List Pane** | souhrn každého paketu – zdroj, cíl, protokol, info; kliknutím vybereš paket |
| **Packet Details Pane** | detailní **rozpis protokolů** vybraného paketu (podle TCP/IP) |
| **Packet Bytes Pane** | **hex + ASCII** podoba paketu; zvýrazní část, na kterou klikneš v detailech |

![[ws_bas_nacteny_pcap.png|650]]

### Zabarvení paketů

- Wireshark barví pakety podle **protokolu a podmínek** → rychlé odhalení anomálií
- dva typy pravidel:
  1. **dočasná** – jen během relace (pravý klik / **View → Conversation Filter**)
  2. **trvalá** – uložená v **profilu** (pravý klik / **View → Coloring Rules…**)
- **View → Colourise Packet List** = zapne/vypne barvení

**Výchozí barvy**

![[ws_bas_zabarveni.png|650]]

### Zachytávání provozu

- **modrá žraločí ploutev** = start, **červené** tlačítko = stop, **zelené** = restart
- ve stavovém řádku: použité rozhraní a počet zachycených paketů

![[ws_bas_zachytavani.png|450]]

### Sloučení PCAP

- **File → Merge** – spojí dva soubory do jednoho
- sloučený soubor je potřeba **uložit**, než se s ním pracuje

![[ws_bas_merge.png|450]]

### Detaily souboru

- **Statistics → Capture File Properties** nebo **ikona pcap** vlevo dole
- ukáže: **hash** souboru, čas zachycení, **komentáře** k souboru, rozhraní, statistiky

![[ws_bas_capture_file_properties.png|450]]

## Disekce paketů

- **disekce** = rozklad paketu dekódováním protokolů a jejich polí
- klik na paket → detaily; **dvojklik** → detaily v novém okně
- klik na detail → zvýrazní se odpovídající bajty v Packet Bytes

**Paket 27**

![[ws_bas_paket_detail.png|450]]

**Klik na detail → zvýraznění bajtů**

![[ws_bas_bajty_zvyrazneni.png|450]]

- paket má **5–7 vrstev** podle [[OSI model|modelu OSI]]:

| Vrstva | Co ukazuje |
| :-- | :-- |
| **Frame** (L1) | jaký rámec/paket to je, detaily **fyzické vrstvy** |
| **Source [MAC]** (L2) | zdrojová a cílová **MAC adresa**, protokol síťové vrstvy (Data Link) |
| **Source [IP]** (L3) | zdrojová a cílová **IPv4**, protokol transportní vrstvy |
| **Protocol** (L4) | [[TCP]]/[[UDP]], **zdrojový a cílový port** |
| **Protocol Errors** | pokračování L4 – segmenty [[TCP]], které bylo nutné **znovu sestavit** |
| **Application Protocol** (L5) | detaily aplikačního protokolu – [[HTTP]], FTP, SMB |
| **Application Data** | data konkrétní aplikace |

**Přehled vrstev**

![[ws_bas_vrstvy_prehled.png|450]]

**Frame**

![[ws_bas_vrstva_frame.png|450]]

**Source [MAC]**

![[ws_bas_vrstva_mac.png|450]]

**Source [IP]**

![[ws_bas_vrstva_ip.png|450]]

**Protocol**

![[ws_bas_vrstva_protokol.png|450]]

**Protocol Errors**

![[ws_bas_vrstva_chyby.png|450]]

**Application Protocol**

![[ws_bas_vrstva_aplikace.png|450]]

**Application Data**

![[ws_bas_vrstva_data.png|450]]

## Navigace mezi pakety

### Čísla paketů a Go to Packet

- každý paket má **jedinečné číslo** → snadný návrat k určitému bodu
- **Go to Packet** (menu **Go** / toolbar) – skok na číslo, nahoru/dolů, další paket v konverzaci

**Čísla paketů**

![[ws_bas_cisla_paketu.png|450]]

**Go to Packet**

![[ws_bas_go_to_packet.png|450]]

### Find Packet (Edit → Find Packet)

- hledání podle **obsahu** paketu
- **4 typy vstupu**: display filter, **hex**, **string**, **regex** (nejčastěji string a regex)
- standardně **nerozlišuje velikost písmen** (dá se zapnout)
- je nutné vybrat **správný panel** (Packet List / Details / Bytes) – když hledám v List něco, co je jen v Details, **nic nenajde**

![[ws_bas_find_packet.png|650]]

### Označení, komentáře, export

| Funkce | Popis |
| :-- | :-- |
| **Mark Packets** | označí paket (zobrazí se **černě**); **po zavření souboru se ztratí** |
| **Packet Comments** | komentář k paketu; **zůstává v souboru**, dokud ho někdo nesmaže |
| **Export Packets** | **File** – uloží jen vybrané pakety (sdílení podezřelých paketů) |
| **Export Objects** | **File → Export Objects** – vytáhne **přenesené soubory**; jen pro **DICOM, HTTP, IMF, SMB, TFTP** |
| **Time Display Format** | **View → Time Display Format**; výchozí = sekundy od začátku zachycení, běžně se přepíná na **UTC** |

**Mark Packets**

![[ws_bas_mark_packets.png|650]]

**Packet Comments**

![[ws_bas_packet_comment.png|450]]

**Export Packets**

![[ws_bas_export_packets.png|650]]

**Export Objects**

![[ws_bas_export_objects.png|650]]

**Time Display Format**

![[ws_bas_time_format.png|450]]

![[ws_bas_time_format_2.png|450]]

### Expert Info

- **Analyse → Expert Information** nebo **levý dolní roh** stavového řádku
- Wireshark upozorní na **podezřelé stavy protokolů** – jen **návrhy**, můžou být falešně pozitivní/negativní (viz [[Expert Info]])

| Závažnost | Barva | Info |
| :-- | :-- | :-- |
| **Chat** | modrá | běžný průběh komunikace |
| **Note** | tyrkysová | pozoruhodné události (chybové kódy aplikací) |
| **Warn** | žlutá | varování (neobvyklé chyby, problémy) |
| **Error** | červená | problémy jako **poškozené pakety** |

| Skupina | Info |
| :-- | :-- |
| **Checksum** | chyba kontrolního součtu |
| **Comment** | nalezen komentář paketu |
| **Deprecated** | zastaralý protokol |
| **Malformed** | chybný paket |

![[ws_bas_expert_info.png|650]]

## Filtrování paketů

- dva typy: **[[capture filter|zachytávací]]** (co se uloží) a **[[display filter|zobrazovací]]** (co se ukáže) – detail v [[02_Wireshark_Packet_Operations|další místnosti]]
- zlaté pravidlo: **„Když na to můžeš kliknout, můžeš to filtrovat a kopírovat."**

| Funkce | Co dělá | Kde |
| :-- | :-- | :-- |
| **Apply as Filter** | filtruje **jednu hodnotu** pole; filtr se hned použije | pravý klik / **Analyse → Apply as Filter** |
| **Conversation Filter** | ukáže jen pakety **stejné konverzace** (IP + porty) | pravý klik / **Analyse → Conversation Filter** |
| **Colourise Conversation** | konverzaci jen **obarví**, nic neskryje | **View → Colourise Conversation** (reset: Reset Colourisation) |
| **Prepare as Filter** | filtr jen **připraví** do lišty, čeká na Enter / `and` / `or` | pravý klik |
| **Apply as Column** | z pole udělá **sloupec** v Packet List | pravý klik / **Analyse → Apply as Column** |
| **Follow Stream** | složí pakety zpět do **dat aplikace** (viz [[Follow Stream]]) | pravý klik / **Analyse → Follow TCP/UDP/HTTP Stream** |

**Apply as Filter**

![[ws_bas_apply_as_filter.png|650]]

**Conversation Filter**

![[ws_bas_conversation_filter.png|650]]

**Colourise Conversation**

![[ws_bas_colourise_conversation.png|450]]

**Prepare as Filter**

![[ws_bas_prepare_as_filter.png|650]]

**Apply as Column**

![[ws_bas_apply_as_column.png|650]]

**Follow Stream**

![[ws_bas_follow_stream.png|650]]

- **Follow Stream**: pakety od **klienta červeně**, od **serveru modře**; je vidět i nešifrovaný obsah (jména, hesla)
- po Follow Stream se automaticky nastaví filtr → smazat ho tlačítkem **X** vpravo v liště
- počet **celkových a zobrazených** paketů je vždy ve stavovém řádku

## Otázky z místnosti (Exercise.pcapng)

| Otázka | Odpověď |
| :-- | :-- |
| soubor pro screenshoty / pro otázky | `http1.pcapng` / `Exercise.pcapng` |
| flag v capture file comments | `TryHackMe_Wireshark_Demo` |
| celkový počet paketů | `58620` |
| SHA256 souboru | `f446de335565fb0b0ee5e5a3266703c778b2f3dfad7efeaeccb2da5641a6d6eb` |
| paket 38 – značkovací jazyk pod HTTP | `eXtensible Markup Language` |
| datum doručení paketu | `05/13/2004` |
| TTL | `47` |
| TCP payload | `424` |
| e-tag | `9a01a-4696-7e354b00` |
| „r4w" v detailech – artist 1 | `r4w8173` |
| komentář paketu 12 | `911cd574a42865a956ccde2d04495ebf` |
| jméno „alien" z .txt souboru | `PACKETMASTER` |
| počet varování v Expert Info | `1636` |
| paket 4 → HTTP Apply as Filter – dotaz | `http` |
| počet zobrazených paketů | `1089` |
| paket 33790 Follow Stream – počet umělců | `3` |
| druhý umělec | `Blad3` |

## Související

[[Wireshark]] · [[Wireshark souhrn]] · [[PCAP]] · [[capture filter]] · [[display filter]] · [[Follow Stream]] · [[Expert Info]] · [[Wireshark příkazy]] · [[Wireshark cvičení]] · [[02_Wireshark_Packet_Operations|Packet Operations]] · [[03_Wireshark_Traffic_Analysis|Traffic Analysis]]
