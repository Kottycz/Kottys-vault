# Síťová vrstva

Síťová vrstva ([[OSI]] Layer 3) poskytuje služby, které umožňují koncovým zařízením výměnu dat napříč sítěmi. Mezi další protokoly patří směrovací protokoly ([[OSPF]]) a protokoly pro zasílání zpráv ([[ICMP]]).

- **Adresování** – koncová zařízení musí mít jedinečnou [[IP adresa|IP adresu]].
- **[[zapouzdření|Zapouzdření]]** – síťová vrstva zapouzdřuje [[PDU]] z transportní vrstvy do paketu (provádí zdroj IP paketů).
- **Směrování** – směrování paketů k cílovému hostiteli v jiné síti.
- **Dezapouzdření** – po dezapouzdření paketu síťovou vrstvou je výsledný PDU vrstvy 4 předán transportní vrstvě (provádí cílový hostitel).

## Charakteristiky IP

- **Nespojovaně** – nenavazuje spojení, funguje bezstavově.
- **Nespolehlivě** – nestará se o poškození nebo ztrátu dat.
- **Best effort** – všem datům měří stejně.

Negarantuje, že:
- data vůbec přenese,
- data stihne přenést včas,
- data bude přenášet pravidelně (stejné zpoždění/[[latency|latence]]),
- data doručí ve správném pořadí.

## Paket IPv4 – záhlaví

[[IPv4]] je jeden z primárních protokolů síťové vrstvy. Záhlaví paketu zajišťuje doručení na další místo na cestě k cíli.

Důležitá pole:
- **Verze** – 4bitová hodnota 0100, identifikuje paket jako IPv4.
- **Diferencované služby (DiffServ/DS)** – dříve ToS. 8bitové pole priority (6 bitů [[DSCP]] + 2 bity ECN).
- **[[TTL]] (Time To Live)** – 8bitová hodnota omezující životnost paketu. Nastaví ji zdroj, každým průchodem [[router|routerem]] se sníží o 1. Při dosažení nuly je paket zahozen a odešle se [[ICMP]] „Time Exceeded", router zároveň přepočítá kontrolní součet záhlaví.
- **Protokol** – 8bitová hodnota určující protokol vyšší vrstvy (ICMP=1, [[TCP]]=6, [[UDP]]=17).
- **Kontrolní součet záhlaví** – detekce poškození záhlaví.
- **Zdrojová/cílová IPv4 adresa** – 32bitové hodnoty. Cílová může být [[unicast]], [[multicast]] nebo [[broadcast]].

## Paket IPv6

Výhody [[IPv6]] oproti IPv4:
- **Zvětšený adresní prostor** – 128bitové hierarchické adresování oproti 32bitovému u IPv4.
- **Vylepšené zpracování paketů** – zjednodušené záhlaví s méně poli.
- **Eliminace potřeby [[NAT]]** – díky obrovskému množství veřejných adres, umožňuje end-to-end konektivitu.

## Jak hostitel směřuje (Host Routes)

U IPv4 se pakety vždy vytvářejí na zdrojovém hostiteli, koncová zařízení mají vlastní směrovací tabulku. Hostitel může poslat paket:
- **sám na sebe** – testuje TCP/IP stack (viz [[loopback]]),
- **lokálnímu hostiteli** – cíl ve stejné lokální síti, stejná síťová adresa,
- **vzdálenému hostiteli** – cíl v jiné síti, odlišná síťová adresa.

Příklad: síť `192.168.10.0/24`, číslo sítě `192.168.10.0`, 256 hostů, router `192.168.10.1`, broadcast `192.168.10.255`. PC1 posílá na `192.168.10.3` → stejná síť. PC1 posílá na `10.10.10.2` → jiná síť.

- V IPv4 – zdroj určuje cíl podle vlastní [[maska podsítě|masky podsítě]] + vlastní a cílové IP adresy.
- V IPv6 – lokální router oznamuje lokální síťovou adresu (prefix) všem zařízením (viz [[RA]]).

Směrování = proces identifikace nejlepší cesty k cíli. Router připojený k lokálnímu segmentu = **výchozí brána ([[default gateway]])**.

### Default Gateway

Síťové zařízení, které směruje provoz do jiných sítí. Obvykle router s vlastnostmi:
- lokální [[IP adresa]] ve stejném rozsahu jako ostatní hostitelé v síti,
- přijímá data do lokální sítě a přeposílá data z ní,
- směruje provoz do jiných sítí.

### Směrovací tabulky hostitele

Na Windows: `route print` nebo `netstat -r` (stejný výstup).

- **Seznam rozhraní** – [[MAC adresa]] a číslo rozhraní pro každé síťové rozhraní (Ethernet, Wi-Fi, Bluetooth).
- **Tabulka směrování IPv4** – všechny známé trasy IPv4 (přímá připojení, lokální síť, výchozí trasy).
- **Tabulka směrování IPv6** – totéž pro IPv6.

## Směrování na routeru

Když paket dorazí na rozhraní, router prozkoumá cílovou IP adresu a prohledá směrovací tabulku (seznam známých síťových prefixů a kam přeposlat). Přeposílá podle nejlépe (nejdelší) odpovídající položky trasy.

**Směrovací tabulka routeru obsahuje:**
- **Přímo připojené sítě** – trasy odpovídající aktivním rozhraním routeru. Přidají se automaticky při konfiguraci IP adresy a aktivaci rozhraní.
- **Vzdálené sítě** – trasy k sítím připojeným k jinému routeru. Router se o nich dozví ručně (statické trasy) nebo dynamicky (výměna info přes dynamické směrovací protokoly).
- **Výchozí trasa** – brána poslední záchrany, použije se, když neexistuje lepší shoda.

### Statické směrování

- Trasy nakonfigurované ručně.
- Správce musí trasu ručně upravit při změně [[topologie]].
- Vhodné pro malé sítě s málo/žádnými redundantními spojeními.

### Dynamické směrování

Dynamický směrovací protokol ([[OSPF]], [[EIGRP]], [[BGP]]) umožňuje routerům automaticky se učit o vzdálených sítích (včetně výchozí trasy) od ostatních routerů. Routery si automaticky sdílejí směrovací info a kompenzují změny topologie bez zásahu správce.
