---
aliases: [Class A, Class B, Class C, třídní adresování, classful]
tags: [slovnik]
---

# classful adresování

**Historický způsob dělení [[IPv4]] adres do pevných tříd** s předem danou [[maska podsítě|maskou]]. Dnes nahrazen bezetřídním adresováním ([[délka prefixu|CIDR]]).

---

## Podrobně

### Třídy

| Třída | Rozsah | Pevná maska | Hostů na síť |
| :-- | :-- | :-- | :-- |
| **A** | 0.0.0.0 – 127.255.255.255 | /8 | ~16,7 milionu |
| **B** | 128.0.0.0 – 191.255.255.255 | /16 | 65 534 |
| **C** | 192.0.0.0 – 223.255.255.255 | /24 | 254 |
| D | 224.0.0.0 – 239.255.255.255 | – | [[multicast]] |
| E | 240.0.0.0 – 255.255.255.255 | – | rezervováno |

Třídu šlo poznat rovnou z prvního oktetu – maska se neposílala, protože byla daná.

### Proč to skončilo

Plýtvalo se adresami. Firma se 300 počítači nedostala třídu C (254 adres je málo), takže dostala celou třídu B – **65 tisíc adres**, z nichž využila 300. Zbytek byl nenávratně zablokovaný.

### Co to nahradilo

**CIDR** (Classless Inter-Domain Routing) – libovolná [[délka prefixu]]. Té samé firmě se přidělí `/23` (510 adres), což přesně sedí. Na tom staví i [[VLSM]].

### Pozůstatky v praxi

- **Classful** směrovací protokoly (RIPv1) neposílají masku – dnes se nepoužívají
- Privátní rozsahy pořád odpovídají třídám: 10.0.0.0/8 (A), 172.16.0.0/12 (B), 192.168.0.0/16 (C)
- Termíny "céčková síť" apod. se pořád hovorově používají

**Souvisí:** [[IPv4]], [[maska podsítě]], [[délka prefixu]], [[VLSM]], [[multicast]]
