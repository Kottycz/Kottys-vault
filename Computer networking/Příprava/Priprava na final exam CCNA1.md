# Příprava na final exam CCNA1

Témata z otázek finálního testu **CCNA 1 v7.0 – Introduction to Networks** (60 otázek, 70 % na splnění, 75 min). U každého tématu je **odkaz přímo na místo v zápisu** a za ním pojmy ze slovníku.

Zdroj otázek: [itexamanswers.net – CCNA 1 v7.0 Final Exam](https://itexamanswers.net/ccna-1-v7-0-final-exam-answers-full-introduction-to-networks.html)

---

## 1. Základy sítí a typy sítí

- [x] **peer-to-peer síť vs. P2P aplikace** – síť bez dedikovaného serveru, role se mění podle požadavku; aplikace potřebuje UI a službu na pozadí
  → [[Sitove_komponenty#Peer-to-peer|Síťové komponenty – Peer-to-peer]] · [[Aplikacni_vrstva#Peer-to-Peer sítě|Aplikační vrstva – P2P sítě]] · [[peer-to-peer]]
- [x] sdílená tiskárna doma = **peer-to-peer** model
  → [[Sitove_komponenty#Peer-to-peer|Síťové komponenty – Peer-to-peer]]
- [x] **Internet Messenger** = chat v reálném čase
  → *v zápisech chybí*
- [x] výchozí brána hosta = rozhraní routeru ve stejné síti
  → [[Sitova_vrstva#Default Gateway|Síťová vrstva – Default Gateway]] · [[default gateway]]
- [x] typy sítí (LAN, WAN, internet)
  → [[Bezny_typ_siti]] · [[LAN]] · [[WAN]]

## 2. Spolehlivé sítě a trendy

- [x] **4 charakteristiky sítě**: fault tolerance, škálovatelnost, **QoS**, bezpečnost
  → [[Spolehlive_site#Architektura sítě – čtyři základní charakteristiky|Spolehlivé sítě – čtyři charakteristiky]] · [[QoS]] · [[redundance]] · [[škálování sítě]]
- [x] **pořadí priority QoS**: hlasová konference > finanční transakce > web
  → [[Spolehlive_site#Kvalita služeb (QoS)|Spolehlivé sítě – Kvalita služeb]]
- [x] firemní řešení: **IPS**, **VPN**
  → [[Trendy_a_zabezpeceni_site#Bezpečnostní řešení|Trendy – Bezpečnostní řešení]] · [[IPS]] · [[VPN]] · [[firewall]]

## 3. Protokoly a modely

- [x] **požadavky na zprávu**: velikost, kódování, způsob doručení
  → [[Protokoly_a_modely#Pravidla – požadavky na síťový protokol|Protokoly – požadavky]] · [[Protokoly_a_modely#Možnosti doručování zpráv|Možnosti doručování]]
- [x] **proprietární protokoly** = řídí je jedna firma (např. CDP od Cisco)
  → [[Protokoly_a_modely#Přehled síťových protokolů|Protokoly – přehled]] · [[Budovani_male_site#Příkaz zobrazit sousedy – CDP|CDP]]
- [x] **vrstvy TCP/IP**: aplikační, transportní, internetová, síťový přístup
  → [[Protokoly_a_modely#Sady protokolů|Protokoly – Sady protokolů]] · [[OSI]]
- [ ] aplikační vrstva TCP/IP = OSI **aplikační + prezentační + relační**
  → [[Protokoly_a_modely#Referenční modely|Protokoly – Referenční modely]] · [[Aplikacni_vrstva#Session layer|Session layer]] · [[Aplikacni_vrstva#Presentation layer|Presentation layer]]
- [x] směrování mezi sítěmi = **internetová vrstva**
  → [[Protokoly_a_modely#Internetová vrstva|Protokoly – Internetová vrstva]]
- [x] zapouzdření a PDU
  → [[Protokoly_a_modely#Zapouzdření dat|Protokoly – Zapouzdření dat]] · [[zapouzdření]] · [[PDU]]

## 4. Fyzická vrstva a kabeláž

- [x] rušení měděných kabelů: **EMI, RFI**
  → [[Fyzicka_vrstva#Měděné kabely|Fyzická vrstva – Měděné kabely]] · [[EMI]]
- [x] **útlum (attenuation)** = slábnutí signálu se vzdáleností
  → [[Fyzicka_vrstva#Měděné kabely|Fyzická vrstva – Měděné kabely]] · [[útlum]]
- [x] degradace UTP: **špatné zakončení, nekvalitní kabel/konektory**
  → [[Fyzicka_vrstva#Měděné kabely|Fyzická vrstva – Měděné kabely]] · [[UTP]]
- [x] chyba RJ-45: **příliš dlouhá rozpletená část** drátů
  → [[Fyzicka_vrstva#Měděné kabely|Fyzická vrstva – Měděné kabely]]
- [x] standardy kabeláže: **délky kabelů, typy konektorů, zapojení pinů**
  → [[Fyzicka_vrstva#Měděné kabely|Fyzická vrstva – Měděné kabely]]
- [x] optika
  → [[Fyzicka_vrstva#Optické kabely|Fyzická vrstva – Optické kabely]] · [[optické vlákno]]
- [ ] bezdrát: **ZigBee** (chytrá domácnost), návrh WiFi (pokrytí, rušení, bezpečnost)
  → [[Fyzicka_vrstva#Bezdrátová média|Fyzická vrstva – Bezdrátová média]] · [[ZigBee]] · [[WLAN]]
- [ ] přístup k bezdrátovému médiu = **CSMA/CA**
  → [[Data_link#Metody řízení přístupu|Data link – Metody řízení přístupu]] · [[CSMA-CA]]

## 5. Číselné soustavy

- [x] převody bin ↔ dec ↔ hex (nutné pro podsítě, MAC, IPv6)
  → [[Ciselne_soustavy#Soustavy používané v sítích|Číselné soustavy – v sítích]] · [[Ciselne_soustavy#Převodní tabulka|Převodní tabulka]]

## 6. Linková vrstva (Data link)

- [x] funkce linkové vrstvy = výměna rámců po společném médiu
  → [[Data_link#Vrstva datového spojení|Data link – Vrstva datového spojení]]
- [x] **LLC**: identifikuje protokol síťové vrstvy, umožní IPv4 i IPv6 na stejném médiu
  → [[Data_link#Podvrstvy datového spoje IEEE 802 LAN/MAN|Data link – Podvrstvy]] · [[LLC]]
- [x] **MAC podvrstva**: zapouzdření dat, přístup k médiu, ohraničení rámce, přidání FCS
  → [[Data_link#Podvrstvy datového spoje IEEE 802 LAN/MAN|Data link – Podvrstvy]] · [[Data_link#Providing access to media|Přístup k médiu]] · [[MAC podvrstva]]
- [x] **pole rámce**: adresování, kontrola chyb, typ (protokol L3), začátek rámce
  → [[Data_link#Frame fields|Data link – Frame fields]] · [[Ethernet_Switching#Ethernet Frame Fields|Ethernet Frame Fields]] · [[FCS]] · [[EtherType]] · [[SFD]]
- [x] změněný rámec odhalí **FCS**
  → [[Data_link#Frame fields|Data link – Frame fields]] · [[CRC]]
- [x] router u rámce: **odstraní L2 hlavičku, přidá novou** pro další linku
  → [[Data_link#Vrstva datového spojení|Data link – Vrstva datového spojení]]
- [x] NIC patří do L2 kvůli **MAC adrese**
  → [[Ethernet_Switching#Ethernet MAC Address|Ethernet MAC Address]] · [[NIC]] · [[MAC adresa]]
- [x] half / full duplex
  → [[Data_link#Poloduplexní a plně duplexní komunikace|Data link – Duplex]] · [[full-duplex]] · [[half-duplex]]

## 7. Ethernet switching

- [x] **store-and-forward**: uloží celý rámec, kontroluje CRC, zahodí vadné
  → [[Ethernet_Switching#Metody přepínání|Ethernet Switching – Metody přepínání]] · [[store-and-forward]]
- [x] **cut-through**: nízká latence, posílá hned po cílové adrese, může přeposlat runt; varianta **fragment-free**
  → [[Ethernet_Switching#Metody přepínání|Ethernet Switching – Metody přepínání]] · [[cut-through]]
- [x] při překročení chybovosti přepne switch na **store-and-forward**
  → [[Ethernet_Switching#Metody přepínání|Ethernet Switching – Metody přepínání]]
- [x] switch, duplex a rychlost, Auto-MDIX
  → [[Ethernet_Switching#Základy switchů|Základy switchů]] · [[Ethernet_Switching#Nastavení duplexu a rychlosti|Duplex a rychlost]] · [[Computer networking/Slovnik/switch|switch]] · [[Auto-MDIX]]

## 8. Síťová vrstva

- [x] vlastnosti IP: **bez spojení, nezávislé na médiu**, best effort
  → [[Sitova_vrstva#Charakteristiky IP|Síťová vrstva – Charakteristiky IP]]
- [x] **TTL** – snižuje se, při 0 zahodit + ICMP Time Exceeded
  → [[Sitova_vrstva#Paket IPv4 – záhlaví|Síťová vrstva – IPv4 záhlaví]] · [[TTL]]
- [x] IPv4 vs. IPv6 hlavička: TTL → **Hop Limit**, Source Address zůstává
  → [[Sitova_vrstva#Paket IPv6|Síťová vrstva – Paket IPv6]]
- [x] router: přímo připojená síť → pošle paket ven daným rozhraním
  → [[Sitova_vrstva#Směrování na routeru|Síťová vrstva – Směrování na routeru]] · [[router]]
- [x] špatná výchozí brána → **nefunguje komunikace se vzdálenými sítěmi**
  → [[Sitova_vrstva#Default Gateway|Síťová vrstva – Default Gateway]]
- [x] **NAT** – zpomaluje vyčerpání IPv4, rozbíjí end-to-end aplikace
  → [[IPv4_adresovani#Veřejné a soukromé IPv4 adresy|IPv4 – Veřejné a soukromé adresy]] · [[NAT]]

## 9. Rozlišení adres (ARP, ND)

- [x] **ARP request** = broadcast, když znám IP a neznám MAC; odpověď = ARP reply
  → [[Rozliseni_adres#MAC a IP adresy – přehled ARP|Rozlišení adres – ARP]] · [[ARP]]
- [x] vzdálený cíl → ARP na **MAC výchozí brány**
  → [[Rozliseni_adres#MAC a IP adresy – přehled ARP|Rozlišení adres – ARP]]
- [x] problémy ARP: broadcasty zahlcují síť, všechny uzly zpracovávají request
  → [[Rozliseni_adres#MAC a IP adresy – přehled ARP|Rozlišení adres – ARP]]
- [x] L2 / L3 adresy při cestě přes router (MAC se mění, IP ne)
  → [[Protokoly_a_modely#Data Access – adresy|Protokoly – Data Access adresy]]
- [x] ICMPv6 navíc oproti ICMPv4: **Neighbor Solicitation, Router Advertisement**
  → [[Rozliseni_adres#Vyhledávání souseda přes IPv6|Rozlišení adres – IPv6 ND]] · [[NDP]] · [[NS]] · [[NA]] · [[RA]] · [[RS]]

## 10. IPv4 adresování a podsítě

- [x] **nejmenší maska pro N zařízení**: 4 → /29, 10 → /28, 25 → /27, 61 → /26, 90 → /25, 200 → /24
  → [[IPv4_adresovani#Maska podsítě|IPv4 – Maska podsítě]] · [[IPv4_adresovani#Délka prefixu|Délka prefixu]] · [[maska podsítě]] · [[délka prefixu]]
- [x] přiřazení síť / prefix (např. 192.168.0.128/25, .96/27, .80/30)
  → [[IPv4_adresovani#Příklad – efektivní vytváření podsítí IPv4|IPv4 – vytváření podsítí]]
- [x] do které podsítě patří host (192.168.1.96 → 192.168.1.64/26)
  → [[IPv4_adresovani#Síťové a hostitelské části|IPv4 – Síťová a hostitelská část]]
- [x] jedna maska pro více podsítí (největší 22 hostů → /27)
  → [[IPv4_adresovani#Network Segmentation|IPv4 – Network Segmentation]]
- [x] **/28 podsítě** bez plýtvání (10.18.10.208/28, .224/28)
  → [[IPv4_adresovani#VLSM Basics|IPv4 – VLSM]] · [[VLSM]]
- [x] unicast, broadcast, multicast
  → [[IPv4_adresovani#Unicast, Broadcast nebo Multicast|IPv4 – Unicast, Broadcast, Multicast]] · [[unicast]] · [[broadcast]] · [[multicast]]

## 11. IPv6 adresování

- [ ] **GUA** = global routing prefix + subnet ID + interface ID
  → [[IPv6_adresovani#IPv6 GUA|IPv6 – GUA]] · [[GUA]]
- [ ] subnet ID z adresy (2001:DA48:FC5:A4:3D1B::1/64 → 2001:DA48:FC5:A4::/64)
  → [[IPv6_adresovani#Subnet an IPv6 Network|IPv6 – Subnet]] · [[hextet]]
- [ ] **link-local** = FE80::/10
  → [[IPv6_adresovani#LLA (Link-Local Address) pro IPv6|IPv6 – LLA]] · [[LLA]]
- [ ] **EUI-64** z MAC (vložit FFFE, převrátit 7. bit)
  → [[IPv6_adresovani#Dynamické adresování pro IPv6 LLA|IPv6 – Dynamické LLA]] · [[EUI-64]]
- [ ] **FF02::2** = všechny routery; `ipv6 unicast-routing` → router posílá **RA**
  → [[IPv6_adresovani#IPv6 Multicast Addresses|IPv6 – Multicast adresy]]
- [ ] SLAAC, DHCPv6
  → [[IPv6_adresovani#Dynamické adresování pro IPv6 GUA|IPv6 – Dynamické GUA]] · [[SLAAC]] · [[DAD]]
- [ ] zkracování zápisu
  → [[IPv6_adresovani#Pravidla pro zkracování zápisu|IPv6 – Zkracování]] · [[IPv6]]

## 12. Transportní vrstva

- [ ] doručení dat správné aplikaci (oknu prohlížeče) = transportní vrstva
  → [[Transport_layer#Odpovědnosti transportní vrstvy|Transport – Odpovědnosti]]
- [ ] více relací rozlišují **zdrojové porty**
  → [[Transport_layer#Socket pairs|Transport – Socket pairs]] · [[port]] · [[socket]]
- [ ] TCP i UDP: **čísla portů, checksum**
  → [[Transport_layer#TCP (Transmission Control Protocol)|TCP]] · [[Transport_layer#UDP (User Datagram Protocol)|UDP]] · [[TCP]] · [[UDP]]
- [ ] **sliding window** – žádost o snížení rychlosti přenosu
  → [[Transport_layer#Řízení toku TCP (flow control) – velikost okna a potvrzení|Transport – Řízení toku]] · [[sliding window]]
- [ ] RTP = **hlas a video**
  → *v zápisech chybí* · [[VoIP]]

## 13. Aplikační vrstva a porty

| Port | Protokol | K čemu | Zápis |
| :-- | :-- | :-- | :-- |
| 21 | [[FTP]] | přenos souborů klient–server | [[Aplikacni_vrstva#File Transfer Protocol (FTP)\|FTP]] |
| 25 | [[SMTP]] | odesílání e-mailu | [[Aplikacni_vrstva#E-mailové protokoly\|E-mailové protokoly]] |
| 53 | [[DNS]] | překlad jmen na IP (A, AAAA, NS, MX) | [[Aplikacni_vrstva#Protokoly aplikační vrstvy\|Protokoly aplikační vrstvy]] |
| 67 | [[DHCP]] | přidělení IP | [[Aplikacni_vrstva#Protokol dynamické konfigurace hostitele (DHCP)\|DHCP]] |
| 69 | [[TFTP]] | jednoduchý přenos souborů | [[Aplikacni_vrstva#Protokoly aplikační vrstvy\|Protokoly aplikační vrstvy]] |
| 80 | [[HTTP]] | web | [[Aplikacni_vrstva#HTTP / HTTPS\|HTTP / HTTPS]] |
| 110 | [[POP3]] | stažení e-mailu do klienta | [[Aplikacni_vrstva#E-mailové protokoly\|E-mailové protokoly]] |
| 143 | [[IMAP]] | e-maily zůstávají na serveru | [[Aplikacni_vrstva#E-mailové protokoly\|E-mailové protokoly]] |
| 443 | [[HTTPS]] | šifrovaný web | [[Aplikacni_vrstva#HTTP / HTTPS\|HTTP / HTTPS]] |

- [ ] skupiny portů (well-known, registered, dynamic)
  → [[Transport_layer#Skupiny čísel portů|Transport – Skupiny čísel portů]]
- [ ] **BOOTP** – bezdiskové stanice zjistí IP a server
  → [[Aplikacni_vrstva#Protokol dynamické konfigurace hostitele (DHCP)|Aplikační vrstva – DHCP]] · [[BOOTP]]

## 14. Cisco IOS a konfigurace

- [ ] konfigurace jen z privilegovaného režimu (chyba při zadání v user EXEC)
  → [[Navigace_v_IOSu#Režimy|Navigace v IOSu – Režimy]] · [[IOS]]
- [ ] `service password-encryption` – zašifruje hesla v konfiguraci
  → [[Zakladni_konfigurace_zarizeni#Šifrování hesel|Konfigurace zařízení – Šifrování hesel]]
- [ ] test banneru: odejít z privileged EXEC a zmáčknout Enter
  → [[Zakladni_konfigurace_zarizeni#Zprávy v bannerech|Konfigurace zařízení – Bannery]]
- [ ] `ip default-gateway` na switchi → **vzdálená správa** z jiné sítě
  → [[Konfigurace_IP_adresovani#Konfigurace virtuálního rozhraní přepínače (SVI)|Konfigurace SVI]] · [[SVI]]
- [ ] `show ip interface brief`
  → [[Zakladni_konfigurace_routeru#Ověření konfigurace rozhraní|Konfigurace routeru – Ověření rozhraní]] · [[příkazy show]]
- [ ] **SSH**: doménové jméno, generovat klíče, `transport input ssh` na vty
  → [[Zaklady_sitove_bezpecnosti#Povolení SSH|Bezpečnost – Povolení SSH]] · [[SSH]] · [[Telnet]]
- [ ] running-config vs. startup-config
  → [[Ulozeni_konfiguraci#Konfigurační soubory|Uložení konfigurací]] · [[running-config]] · [[startup-config]]
- [ ] struktura příkazů, nápověda
  → [[Command_Structure#Nápověda|Command Structure – Nápověda]]

## 15. Malá síť a diagnostika

- [ ] Windows příkazy: **ipconfig, ping, nslookup**
  → [[Budovani_male_site#Příkazy na hostiteli|Malá síť – Příkazy na hostiteli]] · [[ipconfig]] · [[nslookup]]
- [ ] ping na IP funguje, na jméno ne → **nslookup** (DNS)
  → [[Budovani_male_site#ping|Malá síť – ping]] · [[ping]]
- [ ] výstup traceroute – počet hopů
  → [[Budovani_male_site#traceroute|Malá síť – traceroute]] · [[traceroute]] · [[hop]]
- [ ] **baseline** výkonu sítě – zjistí, co je normální
  → *v zápisech chybí* · [[baseline]]
- [ ] protocol analyzer: zachytávat ve špičce a na různých segmentech
  → [[Budovani_male_site#IP adresování|Malá síť – IP adresování]] · [[sniffer]]
- [ ] přístup na cisco.com potřebuje **DNS server + výchozí bránu**
  → [[Sitova_vrstva#Default Gateway|Síťová vrstva – Default Gateway]] · [[DNS]]

## 16. Bezpečnost sítě

- [ ] **malware**: virus, trojský kůň, červ
  → [[Zaklady_sitove_bezpecnosti#Typy malwaru|Bezpečnost – Typy malwaru]] · [[malware]] · [[virus]] · [[trojský kůň]] · [[červ (malware)]]
- [ ] **spyware a adware**, **krádež identity**, antivirus a antispyware
  → [[Trendy_a_zabezpeceni_site#Zabezpečení sítě – hrozby|Trendy – hrozby]] · [[spyware]] · [[adware]]
- [ ] doplněk, který vypne firewall = **trojský kůň**
  → [[Zaklady_sitove_bezpecnosti#Trojští koně|Bezpečnost – Trojští koně]]
- [ ] **reconnaissance** – průzkum (i přes WiFi)
  → [[Zaklady_sitove_bezpecnosti#Trojští koně|Bezpečnost – Průzkumné útoky]] · [[reconnaissance]]
- [ ] **DoS** – zpomalí/shodí službu
  → [[Zaklady_sitove_bezpecnosti#Útoky typu odmítnutí služby|Bezpečnost – DoS]] · [[DoS-DDoS]]
- [ ] typy hrozeb: elektrické, hardwarové, prostředí, údržba
  → [[Zaklady_sitove_bezpecnosti|Bezpečnost – úvod (fyzické hrozby)]]
- [ ] obrana: antivirus + aktualizace OS a aplikací
  → [[Zaklady_sitove_bezpecnosti#Aktualizace, upgrade a oprava|Bezpečnost – Aktualizace]]
- [ ] **AAA** – autorizace = co smím
  → [[Zaklady_sitove_bezpecnosti#Ověřování, autorizace a účtování|Bezpečnost – AAA]] · [[AAA]]
- [ ] **funkce firewallu**: filtrování aplikací, paketů, URL, **SPI**
  → [[Zaklady_sitove_bezpecnosti#Firewall|Bezpečnost – Firewall]] · [[firewall]] · [[SPI]]

---

## Souvisí

[[Síťové pojmy]]
