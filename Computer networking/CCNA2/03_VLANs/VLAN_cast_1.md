# VLAN #1

CCNA 2 (SRWE), modul 3, část 1. Viz [[VLAN]], [[Koncepty_prepinani]].

> „VLAN slouží k rozdělení sítě na menší sítě, takže zařízení a lidé v rámci jedné VLAN spolu komunikují a nemusejí spravovat provoz z jiných sítí. Správce sítě může VLAN organizovat podle umístění, kdo je používá, typu zařízení nebo jakékoli potřebné kategorie."

Sítě [[VLAN]] v přepínané síti umožňují uživatelům v různých odděleních (tj. IT, HR a prodej) připojit se ke stejné síti bez ohledu na použitý fyzický [[switch|přepínač]] nebo jeho umístění v kampusové síti [[LAN]]. VLAN vytváří logickou [[broadcast doména|doménu vysílání]], která může zahrnovat více fyzických segmentů LAN. VLAN zlepšují výkon sítě oddělením velkých domén vysílání na menší. Pokud zařízení v jedné VLAN odešle rámec [[broadcast|vysílání]] [[Ethernet|Ethernetu]], všechna zařízení ve VLAN tento rámec přijmou, ale zařízení v jiných VLAN nikoli. Pomocí sítí VLAN mohou správci sítě implementovat zásady přístupu a zabezpečení podle specifických skupin uživatelů. Každý port přepínače lze přiřadit pouze k jedné síti VLAN (s výjimkou portu připojeného k [[VoIP|IP telefonu]] nebo k jinému přepínači).

## Typy VLAN

- [[Default VLAN]]
- [[Data VLAN]]
- [[nativní VLAN|Native VLAN]]
- [[Management VLAN]]
- [[Voice VLAN]]

**[[VLAN trunk|VLAN Trunks]]** - VLAN trunky umožňují šíření veškerého VLAN provozu mezi přepínači. To umožňuje zařízením připojeným k různým přepínačům, ale ve stejné VLAN, komunikovat bez nutnosti použití [[router|routeru]].

Sítě VLAN jsou přidruženy k jednotlivým portům přepínače a konfigurovány na nich. Zařízení připojená k těmto portům nemají pojem VLAN. Tato zařízení jsou však konfigurována s [[IP adresa|IP adresováním]] a jsou členy specifické IP sítě.

**Identifikace VLAN pomocí tagu** - Standardní záhlaví [[Ethernet|ethernetového]] rámce neobsahuje informace o síti VLAN, do které rámec patří. Proto je při umístění ethernetových rámců na kmenovou síť nutné přidat informace o sítích VLAN, do kterých patří. Tento proces, nazývaný tagging (značkování), se provádí pomocí záhlaví [[802.1Q|IEEE 802.1Q]], specifikovaného ve standardu [[IEEE]] 802.1Q. Záhlaví 802.1Q obsahuje 4bajtový tag vložený do původní záhlaví ethernetového rámce, který určuje VLAN, do které rámec patří.

**[[nativní VLAN|Nativní VLAN]]** - Standard IEEE 802.1Q specifikuje nativní VLAN pro kmenové linky, která je standardně nastavena na VLAN 1. Když na kmenový port dorazí neoznačený rámec, je přiřazen k nativní VLAN. Rámce pro správu odesílané mezi přepínači jsou příkladem provozu, který je obvykle neoznačený.

## Vytváření sítí VLAN

Vytváření sítí VLAN, stejně jako většina ostatních aspektů síťování, je otázkou zadání příslušných příkazů:

Sítě VLAN s normálním dosahem na těchto přepínačích jsou číslovány od 1 do 1 005 a sítě VLAN s rozšířeným dosahem jsou číslovány od 1 006 do 4 094.

Konfigurace jsou uloženy ve [[flash]] paměti přepínače v souboru databáze VLAN s názvem `vlan.dat`.

Po konfiguraci pomáhá protokol VLAN trunking ([[VTP]]) synchronizovat databázi VLAN mezi přepínači:

```
vlan vlan-id, name vlan-name - vytvoření

    vlan 100,102,105-107 - create VLANs 100, 102, 105, 106, and 107

switchport mode access, switchport access vlan vlan-id - přiřazení na port

show vlan - zobrazení nastavených VLAN

    show interfaces fa0/18 switchport - detaily k portu

no vlan vlan-id - odstranění
```

Celý soubor `vlan.dat` lze smazat pomocí příkazu `delete flash:vlan.dat` v [[Navigace_v_IOSu|privilegovaném režimu EXEC]]. Zkrácenou verzi příkazu (`delete vlan.dat`) lze použít, pokud soubor `vlan.dat` nebyl přesunut z výchozího umístění. Po vydání tohoto příkazu a opětovném načtení přepínače již žádné dříve nakonfigurované sítě VLAN nebudou přítomny. Tím se přepínač efektivně vrátí do výchozího stavu z výroby, pokud jde o konfigurace sítí VLAN.

Chcete-li obnovit tovární nastavení přepínače Catalyst, odpojte od přepínače všechny kabely kromě konzolového a napájecího kabelu. Poté zadejte příkaz `erase startup-config` privilegovaný EXEC režim následovaný příkazem `delete vlan.dat`.

**Souvisí:** [[VLAN]], [[SVI]], [[Sprava_switche_SVI]], [[startup-config]], [[IOS]], [[Zakladni_konfigurace_zarizeni]], [[Ulozeni_konfiguraci]], [[Navigace_v_IOSu]], [[Ethernet_Switching]], [[Data_link]], [[Koncepty_prepinani]]

**Předchozí:** [[Koncepty_prepinani]]

**Další:** [[VLAN_cast_2]]
