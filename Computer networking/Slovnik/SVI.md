---
aliases: [Switch Virtual Interface, VLAN interface]
tags: [slovnik]
---

# SVI

**Switch Virtual Interface** – virtuální rozhraní na [[switch|switchi]], kterému se přidělí [[IP adresa]]. Slouží ke vzdálené správě switche nebo ke směrování mezi VLANami.

---

## Podrobně

### Proč je potřeba

Switch pracuje na vrstvě 2 a k přeposílání rámců **žádnou IP adresu nepotřebuje**. Aby se na něj ale dalo připojit přes SSH nebo Telnet, musí mít adresu – a ta se nastaví právě na SVI.

### Konfigurace (Cisco)

```
Switch(config)# interface vlan 1
Switch(config-if)# ip address 192.168.1.2 255.255.255.0
Switch(config-if)# no shutdown
Switch(config)# ip default-gateway 192.168.1.1
```

`ip default-gateway` se nastavuje zvlášť – L2 switch nemá směrovací tabulku, potřebuje vědět, kudy ven ze své podsítě.

### Dvě použití

| Použití | Popis |
| :-- | :-- |
| **Správa (management)** | jedna SVI s adresou, aby šel switch spravovat na dálku |
| **Směrování mezi VLAN** | na L3 switchi má SVI každá VLAN a switch mezi nimi směruje (nahrazuje [[router]]) |

### Podmínky, aby SVI naběhlo

- VLAN musí existovat a být aktivní
- Aspoň jeden port ve VLANě musí být aktivní (up)
- SVI nesmí být v `shutdown`

Když SVI nejde nahodit, tohle bývá příčina.

### Doporučení k VLAN 1

Výchozí VLAN 1 se z bezpečnostních důvodů **pro správu nepoužívá** – bývá aktivní na všech portech. V praxi se vytvoří samostatná management VLAN.

**Souvisí:** [[switch]], [[IP adresa]], [[default gateway]], [[router]], [[running-config]]
