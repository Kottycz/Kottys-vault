---
aliases: [Access Point, přístupový bod, AP]
tags: [slovnik]
---

# AP

**Access Point** – bezdrátový přístupový bod. Propojuje klienty [[WLAN|Wi-Fi]] s drátovou sítí. V podstatě "bezdrátový [[switch]]".

---

## Podrobně

### Co dělá

Přijímá rádiové signály od klientů a přeposílá je do kabelové [[LAN]] (a naopak). Pracuje na spojové vrstvě (OSI 2), rámce přeposílá podle [[MAC adresa|MAC adres]].

### Pojmy kolem AP

| Pojem | Význam |
| :-- | :-- |
| **SSID** | název sítě, který klient vidí v seznamu |
| **BSSID** | [[MAC adresa]] samotného AP |
| **Kanál** | frekvence, na které vysílá |
| **WLC** | kontrolér pro centrální správu desítek AP |

### Autonomní vs. řízené AP

- **Autonomní** – každé se nastavuje zvlášť, vhodné pro domácnost nebo malou firmu
- **Řízené (lightweight)** – spravuje je centrálně **WLC**, používá se ve velkých sítích (škola, firma). Umožňuje bezešvý roaming mezi AP a jednotnou konfiguraci.

### Napájení

Často se používá **PoE** (Power over Ethernet, [[IEEE]] 802.3af/at) – AP dostane napájení i data po jednom kabelu, není potřeba zásuvka u stropu.

### AP vs. router

Domácí "Wi-Fi router" kombinuje víc zařízení v jedné krabičce: [[router]] + [[switch]] + AP + [[NAT]] + [[DHCP]]. Samostatné AP naproti tomu jen rozšiřuje existující síť – adresy přiděluje a směruje něco jiného.

### Umístění

AP se dává co nejvýš a doprostřed pokrývané plochy. Signál tlumí zdi (hlavně železobeton), zrcadla a voda. V pásmu 2,4 GHz se sousední AP nesmí překrývat kanály – proto se volí kanály 1, 6 a 11.

**Souvisí:** [[WLAN]], [[LAN]], [[switch]], [[CSMA-CA]], [[MAC adresa]], [[IEEE]]
