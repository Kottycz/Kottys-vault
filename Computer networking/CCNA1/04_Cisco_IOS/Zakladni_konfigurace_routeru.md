# Základní konfigurace routeru

Konfigurace [[router|routeru]] v [[IOS|Cisco IOS]].

## Základní příkazy

**Nastavení názvu zařízení:**
```
Router(config)# hostname R1
```

**Zabezpečený uživatelský režim EXEC (přes konzoli):**
```
Router(config)# enable secret MOJEHESLO
```

**Zabezpečení konzole:**
```
Router(config)# line console 0
Router(config-line)# password MOJEHESLO
Router(config-line)# login
```

**Zabezpečený vzdálený přístup ([[Telnet]] / [[SSH]]):**
```
Router(config)# line vty 0 4
Router(config-line)# password MOJEHESLO
Router(config-line)# login
Router(config-line)# transport input ssh
```

**Zabezpečení všech hesel v konfiguračním souboru:**
```
Router(config-line)# exit
Router(config)# service password-encryption
```

**Zobrazení právního oznámení (banner MOTD):**
```
Router(config)# banner motd #
Vstup povolen pouze autorizovaným osobám!
Jakýkoli neoprávněný přístup bude zaznamenán.
#
```

**Uložení konfigurace:**
```
Router(config)# end
Router# copy running-config startup-config
```

Viz [[running-config]] a [[startup-config]].

**Příklad celého postupu:**
```
Router> enable
Router# configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)# hostname R1
R1(config)#
```

## Konfigurace rozhraní

```
Router(config)# interface type-and-number
Router(config-if)# description description-text
Router(config-if)# ip address ipv4-address subnet-mask
Router(config-if)# ipv6 address ipv6-address/prefix-length
Router(config-if)# no shutdown
```

Zadává se [[IP adresa]] s [[maska podsítě|maskou podsítě]] ([[IPv4]]) nebo adresa s [[délka prefixu|délkou prefixu]] ([[IPv6]]).

## Ověření konfigurace rozhraní

Nejužitečnější příkazy: `show ip interface brief` a `show ipv6 interface brief`.
