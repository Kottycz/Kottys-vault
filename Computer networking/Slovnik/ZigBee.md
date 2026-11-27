---
aliases: [ZigBee, Zigbee]
tags: [slovnik]
---

# ZigBee

**ZigBee** – bezdrátová technologie s nízkou spotřebou a malou rychlostí, používaná hlavně v chytré domácnosti.

*Příklad: chytré žárovky, senzory dveří a termostat komunikují přes ZigBee.*

---

## Podrobně

- standard **IEEE 802.15.4**
- nízká spotřeba → zařízení vydrží roky na baterii
- nízká rychlost přenosu, krátký dosah
- zařízení tvoří síť typu **mesh** (posílají si data navzájem)
- použití: domácí automatizace, IoT, průmyslové senzory

| Technologie | Použití |
| :-- | :-- |
| **ZigBee** | chytrá domácnost, senzory |
| Bluetooth | sluchátka, myš (krátký dosah) |
| WiFi | připojení k internetu ([[WLAN]]) |

### Typy zařízení v síti

| Zařízení | Úloha |
| :-- | :-- |
| **koordinátor** | zakládá síť, jeden v každé síti (často chytrá brána / hub) |
| **router** | přeposílá zprávy dál, napájený ze sítě (chytrá zásuvka, žárovka) |
| **koncové zařízení** | jen posílá a přijímá, na baterii, většinu času spí (senzor dveří) |

### Parametry

- pásmo **2,4 GHz** (v některých zemích i 868 / 915 MHz),
- rychlost do **250 kb/s**,
- dosah jednotky až desítky metrů, mesh síť ho prodlužuje.

### ZigBee vs. Wi-Fi vs. Bluetooth

| | ZigBee | [[WLAN|Wi-Fi]] | Bluetooth |
| :-- | :-- | :-- | :-- |
| spotřeba | velmi nízká | vysoká | nízká |
| rychlost | nízká | vysoká | střední |
| topologie | mesh | hvězda (AP) | point-to-point / malá síť |
| použití | senzory, chytrá domácnost | internet, video | sluchátka, periferie |

**Souvisí:** [[WLAN]], [[IEEE]]
