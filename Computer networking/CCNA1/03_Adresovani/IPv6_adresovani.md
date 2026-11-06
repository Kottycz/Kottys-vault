# IPv6 Adresování

## Dual Stack

Protokoly [[IPv4]] a [[IPv6]] mohou koexistovat ve stejném segmentu sítě. Zařízení s duálním protokolem používají oba současně. Nativní IPv6 znamená, že síť zákazníka má IPv6 připojení ke svému [[ISP]] a může přistupovat k obsahu na internetu přes IPv6.

## Pravidla pro zkracování zápisu

**Pravidlo 1 – vynechání úvodních nul** v jakémkoli [[hextet|hextetu]]:
- `01ab` → `1ab`
- `09f0` → `9f0`
- `0a00` → `a00`
- `00ab` → `ab`

**Pravidlo 2 – dvojitá dvojtečka** `::` se v adrese může použít pouze jednou:
- `2001:db8:0000:abcd:0000:0000:0000:1234` → `2001:db8::abcd:0000:0000:1234` (nahrazena jen jedna skupina nul) → lépe `2001:db8:0:abcd::1234` (nahrazena delší skupina)

## IPv6 GUA

**Globální směrovací prefix** – prefix/síťová část adresy, kterou ISP přiřazuje zákazníkovi nebo lokalitě. ISP obvykle přiřazují prefix /48. Příklad: `2001:db8:acad::/48` – prvních 48 bitů (3 hextety) určuje síť.

**[[GUA]] (Global [[unicast|Unicast]] Address)** – globálně unikátní a směrovatelné adresy, ekvivalent veřejných IPv4 adres.
- ICANN (přes [[IANA]]) přiděluje bloky pěti regionálním registrátorům (RIR).
- V současnosti se přidělují jen GUA s prvními 3 bity 001, tj. blok 2000::/3 (v hex začíná 2 nebo 3).
- Tento rozsah tvoří jen 1/8 celého adresního prostoru IPv6.

**Struktura GUA:**
- **Globální směrovací prefix** – přiřazuje ISP zákazníkovi (obvykle /48).
- **ID podsítě** – mezi prefixem a ID rozhraní. Na rozdíl od IPv4 (kde se bity vypůjčují z hostitelské části) byl IPv6 navržen přímo pro subnetting. Organizace ho používá k identifikaci podsítí.
- **ID rozhraní** – ekvivalent hostitelské části v IPv4. Jeden hostitel může mít víc rozhraní, každé s jednou nebo víc IPv6 adresami.

## LLA (Link-Local Address) pro IPv6

Umožňuje zařízení komunikovat s jinými IPv6 zařízeními na stejném připojení (podsíti) – pakety s [[LLA]] nelze směrovat za toto připojení. Pokud LLA není nakonfigurována ručně, zařízení si ji vytvoří automaticky bez [[DHCP]].

Rozsah: `fe80::/10` (prvních 10 bitů `1111 1110 10xx xxxx`, první hextet fe80–febf).

**Získání LLA:**
- Staticky – ruční konfigurace.
- Dynamicky – zařízení vytvoří vlastní ID rozhraní náhodně nebo metodou [[EUI-64]] (z [[MAC adresa|MAC adresy]]).

## Statická konfigurace GUA na routeru

IPv4: `ip address ip-adresa maska-podsítě`. IPv6: `ipv6 address ipv6-adresa/délka-prefixu`.

Automatické získání GUA: [[SLAAC]] nebo stavový DHCPv6.
LLA staticky: `ipv6 address ipv6-link-local-address link-local`.

## Dynamické adresování pro IPv6 GUA

Zpráva **ICMPv6 [[RA]]** navrhuje zařízení, jak získat GUA (konečné rozhodnutí záleží na OS). RA obsahuje:
- předponu sítě a délku předpony (do jaké sítě zařízení patří),
- adresu výchozí brány (IPv6 [[LLA]], zdrojová adresa zprávy RA),
- adresy [[DNS]] serverů a název domény.

**Metoda 1 – [[SLAAC]]:** zařízení si samo vytvoří GUA bez DHCPv6, spoléhá na [[ICMP|ICMPv6]] RA od lokálního [[router|routeru]]. Bezstavová – žádný centrální server neeviduje přidělené adresy.

**Metoda 2 – SLAAC + bezstavový DHCPv6:** GUA vytvoří SLAAC, LLA routeru (ze zdroje RA) jako [[default gateway]], bezstavový DHCPv6 server jen pro DNS a doménu (GUA nepřiděluje).

**Metoda 3 – Stavový DHCPv6:** LLA routeru jako výchozí brána, stavový DHCPv6 server přidělí GUA, DNS, doménu i další info.

## Dynamické adresování pro IPv6 LLA

Všechna IPv6 zařízení musí mít povolenou LLA. Vytváří se dynamicky pomocí prefixu `fe80::/10` a ID rozhraní přes [[EUI-64]] nebo náhodně generované 64bitové číslo.

**Příkazy:**
```
show ipv6 interface brief
show ipv6 route
```

## IPv6 Multicast Addresses

- `ff02::1` – [[multicast|multicastová]] skupina všech uzlů. Přijímají a zpracují všechna IPv6 rozhraní na spoji. Router sem posílá ICMPv6 RA.
- `ff02::2` – skupina all-routers. Router se stane členem po povolení příkazem `ipv6 unicast-routing`. Přijímají a zpracují všechny IPv6 routery na daném odkazu.

## Subnet an IPv6 Network

Podsítě se dělí pomocí pole ID podsítě (např. 0001 až 0005 pro 5 podsítí). Každá podsíť /64 poskytne mnohem víc adres, než bude kdy potřeba.
