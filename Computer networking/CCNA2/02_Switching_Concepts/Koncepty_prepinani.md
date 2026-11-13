# Koncepty přepínání

CCNA 2 (SRWE), modul 2. Navazuje na [[Ethernet_Switching]] z CCNA1.

**Vstup** – Používá se k popisu portu, kudy rámec vstupuje do zařízení.

**Výstup** – Používá se k popisu portu, který rámce použijí při opuštění zařízení.

[[switch|LAN přepínač]] přesměrovává provoz na základě vstupního portu a cílové [[MAC adresa|MAC adresy]] ethernetového rámce. U LAN přepínače existuje pouze jedna hlavní přepínací tabulka, která popisuje striktní asociaci mezi MAC adresami a porty; proto ethernetový rámec s danou cílovou adresou vždy opouští stejný výstupní port, bez ohledu na vstupní port, do kterého vstupuje.

Tato tabulka je uložena v paměti [[CAM]] (Content Addressable Memory), což je speciální typ paměti používaný ve vysokorychlostních vyhledávacích aplikacích. Z tohoto důvodu se tabulka MAC adres někdy nazývá také tabulka CAM.

Každý rámec, který vstoupí do přepínače, je kontrolován, zda neobsahuje nové informace. To se provádí prozkoumáním zdrojové MAC adresy rámce a čísla portu, přes který rámec vstoupil do přepínače:

- Pokud zdrojová MAC adresa v tabulce MAC adres neexistuje, přidá se do tabulky MAC adresa a číslo příchozího portu.
- Pokud zdrojová MAC adresa existuje, přepínač aktualizuje časovač obnovení pro danou položku. Ve výchozím nastavení většina ethernetových přepínačů uchovává položku v tabulce po dobu pěti minut. Pokud zdrojová MAC adresa v tabulce existuje, ale na jiném portu, přepínač ji považuje za novou položku. Položka je nahrazena stejnou MAC adresou, ale s aktuálnějším číslem portu.

Pokud je cílová MAC adresa unicastová adresa, přepínač bude hledat shodu mezi cílovou MAC adresou rámce a položkou v tabulce MAC adres:

- Pokud je cílová MAC adresa v tabulce, rámce bude přeposláno ven ze zadaného portu.
- Pokud cílová MAC adresa v tabulce není, switch přepošle rámec na všechny porty kromě příchozího portu. Tomu se říká [[neznámý unicast]]. Pokud je cílová MAC adresa broadcast nebo multicast, rámec je také odeslán na všech portech kromě příchozího.

Přepínače vrstvy 2 používají k přepínání rámců jednu ze dvou metod:

- [[store-and-forward]] switching
- [[cut-through]] switching

Ve starších ethernetových segmentech založených na rozbočovačích soupeřila síťová zařízení o sdílené médium. Segmenty sítě, které sdílejí stejnou šířku pásma mezi zařízeními, se nazývají [[kolizní doména|kolizní domény]]. Když se dvě nebo více zařízení v rámci stejné kolizní domény pokusí komunikovat současně, dojde ke kolizi.

## Broadcast Domains

Soubor propojených přepínačů tvoří jednu [[broadcast doména|broadcast doménu]]. Broadcast doménu vrstvy 2 může rozdělit pouze zařízení síťové vrstvy, například router. Routery se používají k segmentaci broadcast domén, ale segmentují i kolizní doménu.

Broadcast je někdy nezbytné pro počáteční lokalizaci jiných zařízení a síťových služeb, ale také snižuje efektivitu sítě. Šířka pásma sítě se využívá k šíření vysílání. Příliš mnoho broadcastů a vysoká zátěž sítě může vést k přetížení, které zpomaluje výkon sítě. Když jsou dva přepínače propojeny dohromady, doména broadcastů se zvětší.

Přepínače LAN mají speciální vlastnosti, které jim pomáhají zmírnit přetížení sítě. Ve výchozím nastavení se propojené porty přepínačů pokoušejí navázat spojení v [[full-duplex|plném duplexu]], čímž eliminují kolizní domény. Každý plně duplexní port přepínače poskytuje plnou šířku pásma zařízení nebo zařízením, která jsou k tomuto portu připojena. Plně duplexní připojení dramaticky zvýšila výkon sítě LAN a jsou vyžadována pro rychlosti Ethernetu 1 Gb/s a vyšší.

**Souvisí:** [[Ethernet_Switching]], [[Porty_duplex_a_Auto_MDIX]], [[duplex]], [[router]], [[kolize]]
