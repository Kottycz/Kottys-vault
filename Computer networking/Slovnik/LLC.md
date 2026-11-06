---
aliases: [Logical Link Control, LLC podvrstva]
tags: [slovnik]
---

# LLC

**Logical Link Control** – horní podvrstva spojové vrstvy (OSI 2). Tvoří rozhraní mezi síťovou vrstvou a konkrétní síťovou technologií.

---

## Podrobně

### Rozdělení spojové vrstvy

Spojová vrstva se dělí na dvě podvrstvy:

| Vrstva | Podvrstva | Co dělá |
| :-- | :-- | :-- |
| Síťová (IP) | – | adresuje napříč sítěmi |
| Spojová – horní | **LLC** (softwarová) | komunikace s vyšší vrstvou |
| Spojová – dolní | **[[MAC podvrstva\|MAC]]** (hardwarová) | adresace, přístup k médiu |
| Fyzická | – | signál na médiu |

### Co dělá LLC

- **Identifikuje protokol vyšší vrstvy** – označí, jestli v rámci jede [[IPv4]], [[IPv6]], [[ARP]]…, aby příjemce věděl, komu obsah předat
- **Odděluje síťovou vrstvu od technologie** – IP tak může běžet po Ethernetu, Wi-Fi i jiných médiích, aniž by o nich muselo cokoliv vědět
- Volitelně řízení toku a potvrzování (v praxi to dnes dělá [[TCP]])

### Standard

Definuje ho **[[IEEE]] 802.2**, zatímco MAC podvrstva je specifická pro technologii:

- IEEE 802.3 – Ethernet
- IEEE 802.11 – Wi-Fi

### V praxi

V běžném Ethernetu se místo LLC hlavičky používá přímo pole [[EtherType]] v rámci, které protokol vyšší vrstvy označí (0x0800 = IPv4, 0x86DD = IPv6, 0x0806 = ARP). LLC hlavička se tak často vůbec nepoužívá – zůstává hlavně jako teoretický model.

**Souvisí:** [[MAC podvrstva]], [[MAC adresa]], [[PDU]], [[NIC]], [[EtherType]], [[IEEE]]
