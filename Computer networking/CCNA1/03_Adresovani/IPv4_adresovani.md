# IPv4 adresování

## Síťové a hostitelské části

Adresa [[IPv4]] je 32bitová hierarchická adresa, skládá se ze síťové a hostitelské části.

- Bity v síťové části musí být shodné pro všechna zařízení ve stejné síti.
- Bity v hostitelské části musí být jedinečné, aby identifikovaly konkrétního hostitele.

## Maska podsítě

[[maska podsítě|Maska podsítě]] je po sobě jdoucí sekvence bitů 1, po níž následuje sekvence bitů 0.

## Délka prefixu

Počet bitů nastavených na 1 v [[maska podsítě|masce podsítě]]. Zapisuje se v „lomítkové notaci" – lomítko (/) a počet jedničkových bitů (viz [[délka prefixu]]).

## Unicast, Broadcast nebo Multicast

**[[broadcast|Broadcast]]** – dva typy:
- `255.255.255.255` (limited broadcast)
- Directed broadcast, např. na síti `192.168.1.0/24`

**[[multicast|Multicast]]** – IPv4 vyhrazuje rozsah `224.0.0.0`–`239.255.255.255`.

## Veřejné a soukromé IPv4 adresy

Bloky soukromých adres + **[[NAT]] (Network Address Translation)**. Pakety se zdrojovou soukromou IPv4 a cílovou veřejnou adresou musí být před odesláním k [[ISP]] buď filtrovány (zahozeny), nebo přeloženy na veřejnou adresu.

## IPv4 pro speciální použití

**[[loopback|Loopback]] adresy:** `127.0.0.0/8` (127.0.0.1 až 127.255.255.254).

**Legacy Classful Addressing** (viz [[classful adresování]]):
- Class A – rozsah 0.0.0.0/8 až 127.0.0.0/8, pevná maska /8
- Class B – rozsah 128.0.0.0/16 až 191.255.0.0/16, pevná maska /16
- Class C – rozsah 192.0.0.0/24 až 223.255.255.0/24, pevná maska /24

## Network Segmentation

Segment = oblast sítě, kde se šíří [[broadcast|broadcasty]]. Rozdělujeme segmenty podle:
- lokace (patra),
- skupin lidí (admin, student),
- typu zařízení.

## Příklad – efektivní vytváření podsítí IPv4

Síťová adresa `172.16.0.0/22` má 10 hostitelských bitů. Největší podsíť potřebuje 40 hostitelů → minimálně 6 hostitelských bitů (2⁶−2=62 ≥ 40).

Vzorec pro počet podsítí: 2⁴=16 podsítí (potřeba 10, splňuje s rezervou pro růst).

První 4 bity hostitelské části lze použít k alokaci podsítí (2 bity ze 3. oktetu, 2 bity ze 4. oktetu). Pokud jsou ze sítě `172.16.0.0/22` vypůjčeny 4 bity, nová [[délka prefixu]] je `/26` s maskou `255.255.255.192`.

Podsítě lze přiřadit jednotlivým umístěním a připojení mezi [[router|routerem]] a ISP.

## VLSM Basics

Variable-length subnet mask ([[VLSM]]). Příklad: adresní prostor `192.168.20.224/27` má 5 hostitelských bitů; lze si vypůjčit další 3 bity, takže v hostitelské části zůstanou 2 bity – výpočty stejné jako u tradičního subnettingu. Bity se vypůjčí a určí se rozsahy podsítí.

Příklad rozdělení: čtyři podsítě `/27` přiřazeny lokálním [[LAN]] sítím, tři podsítě `/30` přiřazeny mezirouterovým spojům. Toto schéma snižuje počet adres na podsíť na velikost vhodnou pro sítě vyžadující méně podsítí (např. podsíť 7 pro meziroutrové spoje ponechá podsítě 4–6 volné pro budoucí sítě).

## Strukturovaný návrh

- Koncoví uživatelé
- Servery a periferie
- Servery přístupné z internetu
- Zprostředkující zařízení
- Brána

## Subnetting

Postup a cvičení: [[Subnetting]], [[Subnetting - cvičení]].
