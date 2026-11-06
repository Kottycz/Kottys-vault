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

**Souvisí:** [[LAN]], [[CSMA-CA]], [[half-duplex]], [[IEEE]], [[MAC adresa]], [[NIC]]
