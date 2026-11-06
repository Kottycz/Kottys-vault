# Ověřování přímo připojených sítí

Rozcestník [[Basic_Device_Configuration]]. Viz [[Rozhrani_routeru_dual_stack]], [[směrovací tabulka]], [[příkazy show]].

## Stav rozhraní

```
R1# show ip interface brief
Interface           IP-Address      OK? Method Status  Protocol
GigabitEthernet0/0/0 192.168.10.1   YES manual up      up
GigabitEthernet0/0/1 192.168.11.1   YES manual up      up
Serial0/1/0          209.165.200.225 YES manual up     up
Serial0/1/1          unassigned     NO  unset  down    down

R1# show ipv6 interface brief
```

- **Status** = fyzická vrstva, **Protocol** = linková vrstva ([[keepalive]]). **up/up** je OK.
- [[IPv6]] výstup navíc ukazuje **link-local** adresu ([[LLA]], FE80::/10, vzniká automaticky) a globální adresu.

## Směrovací tabulka

```
R1# show ip route
R1# show ipv6 route
```

- **C** = přímo připojená síť (connected).
- **L** = lokální adresa rozhraní (/32 u [[IPv4]], /128 u IPv6).
- Pro každou nakonfigurovanou síť na up/up rozhraní vzniknou dva záznamy: **C** (síť) a **L** (adresa routeru). Viz [[směrovací tabulka]].
- IPv6 [[multicast]] **FF02::** (např. FF02::1 všichni, FF02::2 všechny routery).

## Konfigurace jednoho rozhraní

```
R1# show running-config interface gigabitethernet 0/0/0
```

## Ping

Ověření spojení s koncovými zařízeními, funguje pro IPv4 i IPv6 ([[ping]]):

```
R1# ping 192.168.10.10
R1# ping 2001:db8:acad:1::10
```

## Filtrování výstupu `show`

Výstup delší než 24 řádků se zastaví na `--More--` (**Enter** = další řádek, **mezerník** = další stránka). `terminal length N` nastaví počet řádků, **0 = bez stránkování**.

Za příkaz `show` se dá přidat pipe `|` + parametr + výraz:

| Parametr | Co dělá |
|---|---|
| `section` | zobrazí celou sekci, která začíná výrazem |
| `include` | jen řádky, které obsahují výraz |
| `exclude` | všechny řádky **kromě** těch s výrazem |
| `begin` | od prvního řádku, který obsahuje výraz, dál |

```
R1# show running-config | section line vty
line vty 0 4
 password 7 110A1016141D
 login
 transport input all

R1# show ip interface brief | include up
```
