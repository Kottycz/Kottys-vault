---
aliases: [Network Interface Card, síťová karta, síťovka]
tags: [slovnik]
---

# NIC

**Network Interface Card** – síťová karta. Hardware, kterým se zařízení připojuje k síti. Má natvrdo přidělenou [[MAC adresa|MAC adresu]].

---

## Podrobně

### Co dělá

Pracuje na rozhraní fyzické a spojové vrstvy (OSI 1–2):

- převádí data na signál (elektrický, optický, rádiový) a zpět
- skládá a rozebírá **rámce**
- kontroluje [[FCS]] a vadné rámce zahazuje
- filtruje – zpracuje jen rámce určené své MAC adrese (nebo [[broadcast]]/[[multicast]])

### Typy

| Typ | Popis |
| :-- | :-- |
| **Integrovaná** | na základní desce, dnes standard |
| **Rozšiřující karta** | do PCIe slotu (serverové, vícportové) |
| **USB adaptér** | externí, pro notebooky bez portu |
| **Bezdrátová (WNIC)** | Wi-Fi |
| **Virtuální** | ve virtualizaci (VMware, VirtualBox) – vlastní MAC, ale žádný fyzický hardware |

### MAC adresa

Každá NIC má jedinečnou 48bitovou [[MAC adresa|MAC adresu]] vypálenou od výrobce. Jde ji softwarově přepsat (MAC spoofing), fyzická zůstává.

Zobrazení: `ipconfig /all` (Windows), `ip link` (Linux)

### Vlastnosti k nastavení

- **Rychlost** – 10/100/1000 Mb/s, 2,5G, 10G
- **Duplex** – [[full-duplex]] / [[half-duplex]]
- **[[MTU]]** – velikost rámce (jumbo rámce v datacentrech)
- **Autonegotiation** – automatická domluva rychlosti a duplexu

### Kolik jich může být

Zařízení může mít víc síťových karet – server jich mívá několik (redundance, oddělené sítě), [[router]] má minimálně dvě (jedna do LAN, jedna do WAN). Každá je v jiné síti a má vlastní [[IP adresa|IP adresu]].

**Souvisí:** [[MAC adresa]], [[OUI]], [[full-duplex]], [[MTU]], [[FCS]], [[UTP]]
