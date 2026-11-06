# Transport layer

Transportní vrstva je zodpovědná za logickou komunikaci mezi aplikacemi běžícími na různých hostitelích. Zahrnuje navázání dočasné relace mezi dvěma hostiteli a spolehlivý přenos informací pro aplikaci.

## Odpovědnosti transportní vrstvy

- **Segmentace dat a opětovné sestavení segmentů** – transportní vrstva rozděluje data na menší bloky (segmenty/datagramy), které se snáze spravují a přenášejí.
- **Identifikace aplikací** – musí umět oddělit a spravovat více komunikací s různými požadavky na transport.
- **Multiplexování komunikace** – přepínání komunikace.

[[TCP]] (Transmission Control Protocol) – [[FTP]], [[HTTP]], Email.
[[UDP]] (User Datagram Protocol) – [[DNS]].

## TCP (Transmission Control Protocol)

- **Spolehlivý** – zajišťuje, že všechna data dorazí do cíle.
- **Spojovaný.**

TCP zajišťuje spolehlivost a řízení toku pomocí:
- číslování a sledování datových segmentů,
- potvrzení přijatých dat ([[ACK]]),
- opětovného odeslání nepotvrzených dat po určité době,
- sekvencování dat, která mohou dorazit v nesprávném pořadí,
- odesílání dat efektivní rychlostí přijatelnou pro příjemce,
- navázání relace,
- zajištění doručení ve stejném pořadí,
- řízení toku dat.

### TCP hlavička

TCP je stavový protokol – sleduje stav komunikační relace (co odeslal, co bylo potvrzeno). Stavová relace začíná navázáním a končí ukončením. Segment TCP přidává 20 bajtů (160 bitů) režie při [[zapouzdření]] dat aplikační vrstvy.

### Třícestný handshake ([[3-way handshake]])

Funkce:
- zjišťuje, zda je cílové zařízení přítomno v síti,
- ověřuje, zda má cílové zařízení aktivní službu na cílovém [[port|portu]],
- informuje cíl, že zdroj chce navázat komunikační relaci na daném portu.

**[[ISN]] (initial sequence number)** – počáteční pořadové číslo nastavené při navázání relace. Představuje počáteční hodnotu bajtů přenešených do přijímající aplikace; se přenosem se zvyšuje o počet přenesených bajtů.

### Ztráta dat (opakování přenosu)

**Odesílatel:** pro každý segment udržuje časovač (podle střední doby přenosového zpoždění). Pokud se časovač vynuluje bez potvrzení, může:
- znovu odeslat segment a všechny následující (kontinuální potvrzování s návratem), nebo
- znovu odeslat jen nepotvrzený segment (selektivní kontinuální potvrzování).

**Příjemce** funguje ve 2 režimech:
- „in-order" – přijímá jen data v pořadí, ostatní ignoruje, potvrzuje „přijal jsem vše do pozice X" (výchozí, méně efektivní).
- „out-of-order" – přijímá i data mimo pořadí a snaží se je zařadit; potvrzuje přes [[SACK]] (Selective ACK) – jen určitý úsek „od X do Z".

### Řízení toku TCP (flow control) – velikost okna a potvrzení

Řízení toku = množství dat, které cíl může přijmout a spolehlivě zpracovat. Udržuje spolehlivost úpravou rychlosti toku dat mezi zdrojem a cílem. TCP hlavička obsahuje 16bitové pole **velikost okna** – počet bajtů, které lze odeslat před očekáváním potvrzení. Číslo potvrzení = číslo dalšího očekávaného bajtu.

### Metoda okénka ([[sliding window|Sliding Window]])

Odesílatel se dívá na proud dat a posouvá aktivní okénko doprava podle přicházejících potvrzení (ACK).

1. **Čekání na potvrzení** – část dat neodeslaná, část odeslaná (nepotvrzená, v okénku), část potvrzená.
2. **Přijetí ACK** do pozice Z → nový segment zleva může být odeslán, okénko se posune.
3. **Po posunutí** – nové okénko začíná od pozice Z.

Běžná velikost **[[MSS]]** (Maximum Segment Size) při [[IPv4]] je 1460 bajtů. Hostitel ji určí odečtením záhlaví IP a TCP (20 + 20 bajtů) od [[MTU]] Ethernetu (výchozí 1500 bajtů).

### Zabránění přetížení

Při přetížení dochází k opětovnému přenosu ztracených segmentů. Špatně řízený opakovaný přenos přetížení jen zhorší. Pokud zdroj zjistí, že segmenty nejsou potvrzeny (včas), sníží počet bajtů odesílaných před čekáním na potvrzení.

**TCP [[slow start]]:**
- Původně: po navázání spojení obě strany ihned přenášely s maximální intenzitou → často způsobilo zahlcení sítě.
- Řešení – **slow start**: nejprve odeslán jeden segment (stop&wait místo kontinuálního), po kladném potvrzení mohou být odeslány dva segmenty atd., dokud není dosaženo maxima daného velikostí okénka.
- **Congestion Avoidance**: kdykoli TCP nedostane potvrzení včas, chápe to jako zahlcení a „začíná od začátku" – odešle jeden segment a znovu aplikuje slow start.

## UDP (User Datagram Protocol)

- Neposkytuje spolehlivost ani řízení toku.
- Rozděluje na datagramy.
- Není spojovaný.

## Socket pairs

Kombinace zdrojové IP adresy a portu (nebo cílové IP + port) se nazývá **[[socket]]** = [[IP adresa]] + [[port]].

**Socket pair** = 2× (IP adresa + port) + protokol (TCP/UDP): zdrojová IP + zdrojový port, cílová IP + cílový port.

Sockety umožňují rozlišit více procesů běžících na klientovi a víc připojení k serverovému procesu.

### Skupiny čísel portů

- **Well-known ports** (0–1023) – rezervované pro běžné služby (23 TCP [[Telnet]], 80 TCP [[HTTP]], 443 TCP [[HTTPS]]).
- **Registered** (1024–49151) – přiděluje je [[IANA]] konkrétním aplikacím.
- **Dynamic / efemérní** (49152–65535) – OS klienta je přiděluje dynamicky při zahájení připojení.

Příkaz **netstat** – zobrazí aktivní spojení.

### Opětovné sestavení UDP datagramu

UDP jednoduše znovu sestaví data v pořadí, v jakém byla přijata, a přepošle je aplikaci. Pokud je pořadí dat pro aplikaci důležité, musí si to aplikace ohlídat sama.
