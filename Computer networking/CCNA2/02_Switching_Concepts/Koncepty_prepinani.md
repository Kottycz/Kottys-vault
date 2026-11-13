# Koncepty přepínání

CCNA 2 (SRWE), modul 2. Navazuje na [[Ethernet_Switching]] z CCNA1. Viz [[switch]], [[MAC adresa]].

## Vstup a výstup

- **Vstup** (ingress) – port, kudy rámec **vstupuje** do zařízení.
- **Výstup** (egress) – port, kterým rámec **opouští** zařízení.

## Přepínací tabulka

[[switch|LAN přepínač]] přesměrovává provoz podle **vstupního portu** a **cílové MAC adresy** ethernetového rámce.

- Existuje jen **jedna hlavní přepínací tabulka** se striktní asociací MAC adresa ↔ port.
- Rámec s danou cílovou adresou proto **vždy opouští stejný výstupní port**, bez ohledu na vstupní port.
- Tabulka je v paměti **[[CAM]]** (Content Addressable Memory) – speciální paměť pro vysokorychlostní vyhledávání. Proto se tabulce MAC adres říká také **tabulka CAM**.

## Učení MAC adres

Každý příchozí rámec se kontroluje, zda nenese novou informaci. Přepínač zkoumá **zdrojovou MAC adresu** a **číslo příchozího portu**:

- zdrojová MAC v tabulce **není** → přidá se MAC adresa + číslo portu,
- zdrojová MAC v tabulce **je** → obnoví se **časovač** položky (výchozí doba uchování u většiny přepínačů: **5 minut**),
- zdrojová MAC v tabulce je, ale na **jiném portu** → bere se jako nová položka, stará se **nahradí** stejnou MAC s aktuálním portem.

## Přeposílání rámců

Cílová MAC je **[[unicast]]**:

- cílová MAC **je v tabulce** → rámec se pošle ven jen ze zadaného portu,
- cílová MAC **není v tabulce** → rámec se pošle na **všechny porty kromě příchozího** = **[[neznámý unicast]]**.

Cílová MAC je **[[broadcast]]** nebo **[[multicast]]** → rámec jde také na všechny porty kromě příchozího.

## Metody přepínání

Přepínače vrstvy 2 používají jednu ze dvou metod:

- **[[store-and-forward]] switching**
- **[[cut-through]] switching**

Detaily viz [[Ethernet_Switching]].

## Kolizní domény

Ve starších ethernetových segmentech s rozbočovači (huby) soutěžila zařízení o **sdílené médium**. Segmenty sdílející stejnou šířku pásma se nazývají **[[kolizní doména|kolizní domény]]**.

Když se dvě nebo více zařízení ve stejné kolizní doméně pokusí vysílat současně, dojde ke **[[kolize|kolizi]]**.

## Broadcast domény

- Sada propojených přepínačů tvoří **jednu [[broadcast doména|broadcast doménu]]**.
- Broadcast doménu vrstvy 2 může rozdělit jen zařízení **síťové vrstvy**, např. **[[router]]**.
- Router segmentuje broadcast domény, ale i kolizní domény.
- Propojením dvou přepínačů se broadcast doména **zvětší**.

Broadcast je někdy nezbytný pro počáteční nalezení jiných zařízení a síťových služeb, ale **snižuje efektivitu sítě**: šířka pásma se využívá k šíření broadcastu. Příliš mnoho broadcastů a vysoká zátěž vedou k **přetížení**, které zpomaluje síť.

## Zmírnění přetížení

- Ve výchozím nastavení se propojené porty přepínačů snaží navázat spojení v **[[full-duplex|plném duplexu]]** → **eliminuje kolizní domény**.
- Každý plně duplexní port dává připojenému zařízení **plnou šířku pásma**.
- Plný duplex dramaticky zvyšuje výkon LAN a je **vyžadován od rychlosti 1 Gb/s** výš.

**Souvisí:** [[Ethernet_Switching]], [[Porty_duplex_a_Auto_MDIX]], [[duplex]], [[CAM]], [[kolizní doména]], [[broadcast doména]]
