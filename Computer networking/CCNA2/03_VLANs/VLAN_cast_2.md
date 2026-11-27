# VLAN #2

CCNA 2 (SRWE), modul 3, část 2. Viz [[VLAN]], [[VLAN_cast_1]].

## VLAN Trunks

[[VLAN trunk]] je propojení [[Data_link|vrstvy 2]] mezi dvěma [[switch|přepínači]], které přenáší provoz pro všechny [[VLAN]] (pokud není seznam povolených VLAN omezen ručně nebo dynamicky).

[[Command_Structure|Konfiguračních příkazy]]:

```
interface interface-id

switchport mode trunk

switchport trunk native vlan vlan-id

switchport trunk allowed vlan vlan-list

end
```

Zrušení: `no switchport trunk allowed`, `no switchport trunk native vlan`

[[Overovani_switche_a_chyby_rozhrani|Verifikační příkazy]]:

```
show interfaces interface-ID switchport
```

## Dynamic Trunking Protocol (DTP)

[[DTP]] může urychlit proces konfigurace pro správce sítě. Rozhraní [[Ethernet|ethernetových]] trunkingových sítí podporují různé režimy trunkingu. Rozhraní lze nastavit na trunking nebo netrunking, nebo na vyjednávání trunkingu se sousedním rozhraním. Vyjednávání trunkingu je spravováno protokolem DTP, který funguje pouze na bázi point-to-point mezi síťovými zařízeními.

DTP spravuje vyjednávání trunku pouze v případě, že je port na sousedním [[switch|přepínači]] nakonfigurován v režimu trunku, který podporuje DTP. Přepínače od jiných dodavatelů DTP nepodporují.

[[Command_Structure|Konfiguračních příkazy]]:

```
switchport mode dynamic auto - povolení dynamického trunkingového protokolu

switchport mode trunk - je vždy zapnutý

switchport mode trunk, switchport nonegotiate - povolit trunking z přepínače Cisco do zařízení, které nepodporuje DTP (nebude generovat rámce DTP)
```

Viz.tabulka kombinací nastavení pro obě strany.

[[Overovani_switche_a_chyby_rozhrani|Verifikační příkazy]]:

```
show dtp interfaces
```

**Souvisí:** [[VLAN]], [[VLAN trunk]], [[DTP]], [[nativní VLAN]], [[802.1Q]], [[Data_link]], [[Sprava_switche_SVI]], [[Zakladni_konfigurace_zarizeni]], [[Navigace_v_IOSu]], [[příkazy show]], [[Koncepty_prepinani]]

**Předchozí:** [[VLAN_cast_1]]

**Další:** [[Inter_VLAN_Routing_cast_1]]
