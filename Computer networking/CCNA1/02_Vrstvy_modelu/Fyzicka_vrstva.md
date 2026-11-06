# Fyzická vrstva

## Kódování

Ethernet `100BASE-TX` používá kódování 4B/5B, `1000BASE-T` používá kódování 8B/10B.

## Šířka pásma

Digitální [[šířka pásma]] měří množství dat, které můžou proudit z jednoho místa na druhé za daný čas.

## Měděné kabely

**Charakteristika:** elektromagnetické rušení ([[EMI]]) nebo rádiofrekvenční rušení ([[EMI|RFI]]), přeslech.

**Typy:**
- Nestíněná kroucená dvojlinka ([[UTP]])
- [[STP kabel|Stíněná kroucená dvojlinka]] (STP)
- Koaxiální kabel

**Standardy a konektory pro UTP kabely (kategorie):**
- Kategorie 3 – původně hlasová komunikace, později i data.
- Kategorie 5 – 100 Mb/s.
- Kategorie 5e – 1000 Mb/s.
- Kategorie 6 – přidaný oddělovač mezi páry vodičů, až 10 Gb/s.
- Kategorie 7 – také až 10 Gb/s.
- Kategorie 8 – až 40 Gb/s.

Konektory: zástrčky a zásuvky RJ-45 UTP.

**Přímé a křížené UTP kabely:**
- **Přímý ethernetový kabel** – nejběžnější typ, propojení hostitel–[[switch|přepínač]], přepínač–[[router]].
- **Křížený ethernetový kabel** – propojení podobných zařízení (přepínač–přepínač, hostitel–hostitel, router–router). Dnes už spíš zastaralé, protože síťové karty používají [[Auto-MDIX|auto-MDIX]] k automatické detekci typu kabelu.

## Optické kabely

**Výhody:** menší útlum, plná imunita vůči [[EMI]] a RFI. [[optické vlákno|Optické vlákno]] je flexibilní, extrémně tenké průhledné vlákno z čistého skla (o málo větší než lidský vlas). Funguje jako vlnovod („světlovod") pro přenos světla s minimální ztrátou signálu.

**Typy vláknitých médií:**
- Jednovidové vlákno ([[optické vlákno|SMF]])
- Multimódové vlákno ([[optické vlákno|MMF]])

**Použití optických kabelů:**
- Podnikové sítě – páteřní kabeláž, propojení infrastrukturních zařízení.
- Fiber-to-the-Home ([[optické vlákno|FTTH]]) – širokopásmové připojení domácnostem a malým firmám.
- Dálkové sítě – propojení zemí a měst poskytovateli služeb.
- Podmořské kabelové sítě.

## Bezdrátová média

Bezdrátové připojení je dnes primární způsob připojení k domácím i podnikovým sítím.

**Typy:** Wi-Fi ([[IEEE]] 802.11), Bluetooth (IEEE 802.15), WiMAX (IEEE 802.16), Zigbee (IEEE 802.15.4).

**Bezdrátová lokální síť ([[WLAN]]):** bezdrátový přístupový bod ([[AP]]) koncentruje bezdrátové signály od uživatelů a připojuje je ke stávající síťové infrastruktuře na měděných kabelech (např. Ethernet).
