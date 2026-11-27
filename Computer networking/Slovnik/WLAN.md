---
aliases: [Wireless LAN, Wi-Fi, bezdrátová síť]
tags: [slovnik]
---

# WLAN

**Wireless Local Area Network** – bezdrátová obdoba [[LAN]]. Definuje ji standard [[IEEE]] 802.11, běžně se jí říká **Wi-Fi**.

---

## Podrobně

### Prvky sítě

| Prvek | Popis |
| :-- | :-- |
| **AP** (Access Point) | přístupový bod – "bezdrátový [[switch]]" |
| **SSID** | název sítě, který vidíš v seznamu |
| **BSSID** | [[MAC adresa]] přístupového bodu |
| **Klient** | zařízení s bezdrátovou [[NIC]] |
| **WLC** | kontrolér pro centrální správu víc AP (velké sítě) |

### Pásma a kanály

| Pásmo | Dosah | Rychlost | Rušení |
| :-- | :-- | :-- | :-- |
| **2,4 GHz** | větší | nižší | hodně (mikrovlnky, Bluetooth) |
| **5 GHz** | menší | vyšší | méně |
| **6 GHz** (Wi-Fi 6E/7) | nejmenší | nejvyšší | nejméně |

V pásmu 2,4 GHz se nepřekrývají jen kanály **1, 6 a 11** – proto se v praxi používají právě ty.

### Přístup k médiu

Wi-Fi je [[half-duplex]] – zařízení nemůže vysílat a poslouchat zároveň. Kolizím předchází [[CSMA-CA]]. Proto je reálná rychlost výrazně nižší než deklarovaná a klesá s počtem připojených zařízení.

### Zabezpečení

| Standard | Stav |
| :-- | :-- |
| WEP | **prolomený**, nepoužívat |
| WPA | zastaralý |
| **WPA2** | běžný standard (AES) |
| **WPA3** | aktuální, nejbezpečnější |

### WLAN vs. LAN

| | WLAN | [[LAN]] |
| :-- | :-- | :-- |
| Médium | rádio (sdílené) | kabel |
| Duplex | half | full |
| Kolize | řeší [[CSMA-CA]] | nevznikají |
| Bezpečnost | signál slyší okolí | fyzický přístup ke kabelu |
| Mobilita | vysoká | žádná |

### Generace Wi-Fi

| Generace | Standard | Pásma | Max. teoretická rychlost |
| :-- | :-- | :-- | :-- |
| Wi-Fi 4 | 802.11n | 2,4 / 5 GHz | 600 Mb/s |
| Wi-Fi 5 | 802.11ac | 5 GHz | ~3,5 Gb/s |
| Wi-Fi 6 / 6E | 802.11ax | 2,4 / 5 / (6) GHz | ~9,6 Gb/s |
| Wi-Fi 7 | 802.11be | 2,4 / 5 / 6 GHz | desítky Gb/s |

Reálná rychlost je mnohem nižší a dělí se mezi všechna zařízení v dosahu AP.

### Ad hoc vs. infrastructure

- **infrastructure** – klienti se připojují k [[AP]] (běžný režim),
- **ad hoc** – zařízení se spojí přímo mezi sebou bez AP,
- **tethering / hotspot** – telefon funguje jako AP a sdílí mobilní data.

### Řízený provoz ve firmě

Ve větších sítích AP řídí **WLC** (Wireless LAN Controller): jedna konfigurace pro všechna AP, plynulý roaming mezi AP, automatické nastavení kanálů a výkonu.

**Souvisí:** [[LAN]], [[CSMA-CA]], [[half-duplex]], [[IEEE]], [[MAC adresa]], [[NIC]]
