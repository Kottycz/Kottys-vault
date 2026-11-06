# Ethernet Switching

## Zapouzdření Ethernetu

Ethernet podporuje [[šířka pásma|šířky pásma]] 10 Mb/s–100 Mb/s (a víc).

## Ethernet Frame Fields

- **Preambule a [[SFD]] (Start Frame Delimiter)** – preambule (7 bajtů) a SFD (1 bajt) slouží k synchronizaci mezi odesílajícím a přijímajícím zařízením. Prvních 8 bajtů rámce upozorňuje na příchod nového rámce.
- **Cílová [[MAC adresa]]** (6 bajtů) – identifikuje zamýšleného příjemce. Zařízení porovná adresu se svou MAC – při shodě rámec přijme. Může být [[unicast]], [[multicast]] nebo [[broadcast]].
- **Zdrojová MAC adresa** (6 bajtů) – identifikuje [[NIC]]/zařízení, které rámec odesílá.
- **Typ / Délka** (2 bajty) – určuje protokol vyšší vrstvy v rámci (0x800 [[IPv4]], 0x86DD [[IPv6]], 0x806 [[ARP]]). Označuje se i [[EtherType]].
- **Data** (46–1500 bajtů) – zapouzdřená data z vyšší vrstvy. Pokud je rámec menší než 64 bajtů, přidávají se výplňové bity (pad).
- **[[FCS]] (Frame Check Sequence)** (4 bajty) – detekce chyb pomocí [[CRC]]. Odesílatel vloží CRC, příjemce ho přepočítá a porovná; při neshodě je rámec zahozen.

## Ethernet MAC Address

[[MAC adresa]] identifikuje fyzická zdrojová a cílová zařízení (NIC) v segmentu lokální sítě, na datové vrstvě [[OSI]] modelu. Je 48bitová, vyjádřená 12 hexadecimálními číslicemi.

Výrobce při přiřazení MAC adresy:
- použije svůj přidělený [[OUI]] jako prvních 6 hex číslic,
- přiřadí unikátní hodnotu na posledních 6 hex číslic.

Příklad: [[IEEE]] přiřadilo Ciscu OUI `00-60-2F`. Cisco nakonfiguruje zařízení s unikátním kódem, např. `3A-07-BC` → výsledná MAC adresa `00-60-2F-3A-07-BC`.

**[[unicast|Unicast]] MAC Address** – jedinečná adresa pro odeslání rámce z jednoho zařízení do jednoho cíle.

**[[broadcast|Broadcast]] MAC Address** – přijímán a zpracován každým zařízením v Ethernet [[LAN]].
- Cílová MAC adresa `FF-FF-FF-FF-FF-FF` (48 jedniček v binární soustavě).
- Zahltí všechny porty [[switch|přepínače]] kromě příchozího.
- Není přeposílán [[router|routerem]].

**[[multicast|Multicast]] MAC Address** – přijímán a zpracováván skupinou zařízení patřících do stejné multicastové skupiny.

## Základy switchů

**Tabulka MAC adres** – [[switch]] se učí MAC adresy a podle nich přeposílá rámce.

### Metody přepínání

- **Store-and-forward switching** – přijme se celý rámec, zpracuje se jako celek, rozhodne se, kam se bude přeposílat, a přepošle se.
- **Cut-through switching** – nečeká se na celý rámec, rozhodnutí o přesměrování se udělá hned při příjmu.
  - **Fast-forward switching** – okamžitě přeposílá po přečtení cílové adresy.
  - **Fragment-free switching** – počká na prvních 64 bajtů, pak se rozhodne.

### Memory Buffering on Switches

- **Port-based memory**
- **Shared memory** – sdílená paměť přes všechny porty.

## Nastavení duplexu a rychlosti

**Mechanismy autodetekce** – ethernetové mechanismy umožňující automaticky se dohodnout na parametrech komunikace (autonegotiation) – rychlost a [[full-duplex|duplex]].

**Detekce typu kabelu [[Auto-MDIX]]** – síťové karty dokážou automaticky detekovat typ kabelu (rozhraní MDI a MDIX).
