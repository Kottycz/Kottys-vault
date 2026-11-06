# Správa switche (SVI)

Rozcestník [[Basic_Device_Configuration]]. Viz [[SVI]], [[VLAN]], [[IP adresa]], [[default gateway]].

Pro vzdálenou správu musí mít switch **[[SVI]]** (switch virtual interface) s [[IPv4]] adresou a maskou, nebo [[IPv6]] adresou a délkou prefixu. SVI je **virtuální rozhraní**, ne fyzický port. Ze **vzdálené sítě** musí mít switch navíc **[[default gateway]]**.

Výchozí je správa přes **VLAN 1** (všechny porty jsou ve VLAN 1). Best practice: použít **jinou VLAN** pro správu, např. VLAN 99.

## Topologie

- PC1 – S1 (SVI VLAN 99: `172.17.99.11/24`, `2001:db8:acad:99::11/64`) – R1 (`172.17.99.1`, `2001:db8:acad:99::1/64`)

## Krok 1 – rozhraní pro správu

```
S1# configure terminal
S1(config)# interface vlan 99
S1(config-if)# ip address 172.17.99.11 255.255.255.0
S1(config-if)# ipv6 address 2001:db8:acad:99::11/64
S1(config-if)# no shutdown
S1(config-if)# end
```

**Pozor:**

- SVI VLAN 99 nebude **up/up**, dokud VLAN 99 neexistuje a není ve VLAN 99 připojené zařízení na portu.
- U Catalyst 2960 s IOS 15.0 je pro IPv6 nutné `sdm prefer dual-ipv4-and-ipv6 default` a pak **reload** (viz [[dual-stack]]).

## Krok 2 – default gateway

```
S1# configure terminal
S1(config)# ip default-gateway 172.17.99.1
S1(config)# end
S1# copy running-config startup-config
```

IPv6 default gateway se **nenastavuje** – switch ji získá z **router advertisement** ([[RA]]). Uložení viz [[running-config]], [[startup-config]], [[Ulozeni_konfiguraci]].

## Krok 3 – ověření

```
S1# show ip interface brief
Interface     IP-Address      OK? Method Status    Protocol
Vlan99        172.17.99.11    YES manual down      down

S1# show ipv6 interface brief
Vlan99        [down/down]
    FE80::C27B:BCFF:FEC4:A9C1
    2001:DB8:ACAD:99::11
```

IP adresa na SVI slouží **jen ke vzdálené správě**, switch podle ní nesmí routovat pakety L3. Další krok: [[Telnet_a_SSH]].
