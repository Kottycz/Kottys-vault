# Data link

## Vrstva datového spojení

Spojová vrstva modelu [[OSI]] (vrstva 2):
- zodpovědná za komunikaci mezi síťovými kartami ([[NIC]]),
- umožňuje vyšším vrstvám přístup k médiím,
- řídí, jak jsou data umisťována a přijímána na médium,
- provádí detekci chyb a odmítá poškozený frame.

## Podvrstvy datového spoje [[IEEE]] 802 LAN/MAN

- **[[LLC]] (Logical Link Control)** – podvrstva IEEE 802.2, komunikuje mezi síťovým softwarem vyšších vrstev a hardwarem nižších vrstev. Do rámce umisťuje info, který protokol síťové vrstvy se používá – umožňuje víc protokolům vrstvy 3 ([[IPv4]], [[IPv6]]) používat stejné rozhraní a média.
- **[[MAC podvrstva|MAC]] (Media Access Control)** – implementována hardwarově (IEEE 802.3, 802.11 nebo 802.15). Zodpovědná za [[zapouzdření]] dat a řízení přístupu k médiím, zajišťuje adresování na datové vrstvě, integrována s technologiemi fyzické vrstvy.

## Providing access to media

Na každém hopu podél cesty [[router]] provádí 4 základní Layer 2 funkce:
1. Přijme rámec ze síťového média.
2. Dezapouzdří rámec, aby odkryl zapouzdřený paket.
3. Znovu zapouzdří paket do nového rámce.
4. Přepošle nový rámec na médiu dalšího síťového segmentu.

## Topologie

**[[topologie|Topologie]] [[WAN]]:** Point to point, Hub and spoke, Mesh.

**Topologie [[LAN]]:** Ring, Bus.

## Poloduplexní a plně duplexní komunikace

- **[[half-duplex|Poloduplexní]]** – obě zařízení mohou na médiu vysílat i přijímat, ale ne současně.
- **[[full-duplex|Plně duplexní]]** – obě zařízení mohou vysílat i přijímat současně na sdíleném médiu.

## Metody řízení přístupu

**Přístup založený na konfliktech:**
- [[CSMA-CD|CSMA/CD]] (detekce kolizí) – starší ethernetové [[LAN]] s topologií sběrnice.
- [[CSMA-CA|CSMA/CA]] (předcházení kolizím) – bezdrátové LAN.

**Řízený přístup** – v řízené síti s víc přístupy má každý uzel svůj vlastní čas pro použití média (deterministické, starší typy sítí).

## Frame fields

- **Start/stop indikátory** – identifikují začátek a konec rámce (viz [[SFD]]).
- **Adresování** – zdrojový a cílový uzel na médiu.
- **Typ** – identifikuje protokol vrstvy 3 v datovém poli (viz [[EtherType]]).
- **Control** – identifikuje speciální služby řízení toku, např. [[QoS]] (Quality of Service) – dává prioritu určitým typům zpráv, např. [[VoIP]] je citlivé na zpoždění, proto dostává prioritu.
- **Data** – obsahuje payload rámce (hlavičku paketu, hlavičku segmentu a data).
- **Error Detection** – zařazeno za data, tvoří trailer rámce (viz [[FCS]]).
