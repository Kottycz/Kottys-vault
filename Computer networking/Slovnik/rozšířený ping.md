---
aliases: [extended ping, rozšířený režim ping]
tags: [slovnik]
---

# rozšířený ping

**„Rozšířený" režim příkazu [[ping]] v Cisco [[IOS]]** – umožňuje vytvářet speciální typy pingu úpravou parametrů souvisejících s operací příkazu.

```
Router# ping
```

---

## Podrobně

### Jak se spouští

V privilegovaném režimu se zadá samotné `ping` (bez adresy). IOS se pak postupně ptá na jednotlivé parametry a u otázky na rozšířené příkazy se odpoví `y`:

```
Router# ping
Protocol [ip]:
Target IP address: 192.168.1.1
Repeat count [5]: 10
Datagram size [100]: 1500
Timeout in seconds [2]:
Extended commands [n]: y
Source address or interface: 192.168.2.1
...
```

### Co se dá nastavit

| Parametr | K čemu se hodí |
| :-- | :-- |
| **Repeat count** | kolik zpráv [[echo request]] se pošle |
| **Datagram size** | velikost paketu (test [[MTU]]) |
| **Timeout** | jak dlouho se čeká na odpověď |
| **Source address / interface** | z jaké adresy nebo rozhraní se ping pošle |

### Proč se používá

Běžný ping z routeru jde ze **zdrojové adresy odchozího rozhraní**. Rozšířený ping umožní zvolit **jinou zdrojovou adresu** a tak ověřit, jestli se k cíli dostane provoz i z jiné sítě – například z LAN za routerem.

### Připomenutí

Ping je užitečný pro rychlé zjištění, zda se jedná o problém s připojením na vrstvě 3. Neidentifikuje ale, **kde** se problém podél cesty nachází – na to je [[traceroute]].

### Ukázka

```
R1# ping
Protocol [ip]:
Target IP address: 192.168.2.10
Repeat count [5]: 100
Datagram size [100]: 1500
Timeout in seconds [2]:
Extended commands [n]: y
Source address or interface: 192.168.1.1
Set DF bit in IP header? [no]: yes
...
```

Enter potvrdí výchozí hodnotu v hranatých závorkách.

### Typické použití

- **zdrojová adresa** – ping z LAN rozhraní routeru ověří, že vzdálená síť zná cestu zpátky do tvé LAN (ne jen ke spojovací lince),
- **velký paket s DF bitem** – zjistí problém s [[MTU]] na cestě,
- **mnoho opakování** – zachytí občasné výpadky a ztráty.

### Rychlá varianta

Bez interaktivních otázek: `ping 192.168.2.10 source g0/0/0 repeat 100 size 1500`.

**Souvisí:** [[ping]], [[echo request]], [[IOS]], [[traceroute]], [[MTU]], [[Budovani_male_site]]
