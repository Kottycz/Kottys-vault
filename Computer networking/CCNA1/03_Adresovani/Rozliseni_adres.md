# Rozlišení adres

## MAC a IP adresy – přehled ARP

**[[ARP]] (Address Resolution Protocol)** slouží k mapování [[IPv4]] adres na MAC adresy. V Ethernetových sítích je nutné znát MAC adresu cíle, protože ji ethernetový rámec vyžaduje.

- **Cílová [[MAC adresa]]** – MAC adresa cílového hostitele ve stejném lokálním segmentu. Pokud je cíl v jiné síti, cílovou adresou v rámci je adresa [[default gateway|výchozí brány]] ([[router|routeru]]).
- **Zdrojová MAC adresa** – MAC adresa síťové karty na zdrojovém hostiteli.

Když je paket odeslán do datové vrstvy k [[zapouzdření]] do ethernetového rámce, zařízení hledá v paměťové tabulce MAC adresu namapovanou na IPv4 adresu. Tato tabulka se nazývá **ARP tabulka (ARP cache)** a je dočasně uložena v RAM.

**Postup vyhledávání:**
- Pokud je cílová IPv4 adresa ve stejné síti jako zdrojová, zařízení hledá v ARP tabulce cílovou IPv4 adresu.
- Pokud je cílová adresa v jiné síti, zařízení hledá v ARP tabulce adresu výchozí brány.
- V obou případech se hledá IPv4 adresa a odpovídající MAC adresa.

**Příkaz na ARP tabulku:** `show ip arp` (Cisco) / `arp -a` (Windows).

## Vyhledávání souseda přes IPv6

Ekvivalent ARP v [[IPv6]] ([[NDP]] zprávy):
- [[NS|Neighbor Solicitation]] messages
- [[NA|Neighbor Advertisement]] messages
- [[RS|Router Solicitation]] messages
- [[RA|Router Advertisement]] messages
