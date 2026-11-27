---
aliases: [Media Access Control podvrstva, MAC sublayer]
tags: [slovnik]
---

# MAC podvrstva

**Media Access Control** – dolní podvrstva spojové vrstvy (OSI 2). Řeší fyzickou adresaci, sestavení rámce a pravidla přístupu k médiu.

---

## Podrobně

### Co dělá

| Úkol | Popis |
| :-- | :-- |
| **Sestavení rámce** | přidá [[MAC adresa|MAC adresy]], typ, [[FCS]] |
| **Adresace** | určí zdrojovou a cílovou MAC adresu |
| **Přístup k médiu** | kdo a kdy smí vysílat ([[CSMA-CD]] na drátě, [[CSMA-CA]] u Wi-Fi) |
| **Detekce chyb** | pomocí FCS zahodí poškozené rámce |

### Vztah k LLC

```
Spojová vrstva
├── [[LLC]]  (IEEE 802.2)  – softwarová, komunikuje s IP
└── MAC      (802.3, 802.11) – hardwarová, řeší médium
```

MAC podvrstva je **specifická pro technologii** – Ethernet a Wi-Fi mají každý svoji. LLC je pro obě stejná, a proto může IP běžet po obou bez rozdílu.

### Kde je implementovaná

Přímo v hardwaru [[NIC|síťové karty]] (a v [[switch|switchi]]). Proto je MAC adresa "vypálená" v kartě a operační systém ji jen čte.

### Struktura ethernetového rámce, který MAC sestaví

```
[Preambule][Cíl MAC][Zdroj MAC][EtherType][Data][FCS]
   8 B        6 B       6 B        2 B    46–1500  4 B
```

- **Preambule** – synchronizace příjemce
- **EtherType** – jaký protokol je uvnitř (0x0800 = [[IPv4]])
- **Minimálně 46 B dat** – kratší data se doplní výplní (padding)

### Řízení přístupu k médiu

| Médium | Metoda |
| :-- | :-- |
| klasický Ethernet s huby (half-duplex) | [[CSMA-CD]] |
| Wi-Fi | [[CSMA-CA]] |
| switch, full-duplex | žádná metoda není potřeba, každý má vlastní linku |

### Adresování

MAC podvrstva přidává do rámce zdrojovou a cílovou [[MAC adresa|MAC adresu]]. MAC adresy platí jen v **místní síti**, na každém routeru se rámec rozbalí a pro další úsek se sestaví nový s novými MAC adresami.

### Standardy

MAC podvrstva je pro každou technologii jiná: 802.3 Ethernet, 802.11 Wi-Fi, 802.15 Bluetooth / [[ZigBee]].

**Souvisí:** [[LLC]], [[MAC adresa]], [[FCS]], [[CSMA-CD]], [[CSMA-CA]], [[NIC]]
