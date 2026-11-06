---
aliases: [subnet mask, síťová maska]
tags: [slovnik]
---

# maska podsítě

Určuje, která část [[IPv4]] adresy je **síťová** a která **hostitelská**. Zapisuje se jako `255.255.255.0` nebo prefixem `/24` (viz [[délka prefixu]]).

---

## Podrobně

### Jak funguje

Maska je 32bitové číslo, kde jedničky označují síťovou část a nuly hostitelskou:

```
IP adresa: 192.168.1.10   = 11000000.10101000.00000001.00001010
Maska:     255.255.255.0  = 11111111.11111111.11111111.00000000
                             └───── síť (24 b) ─────┘ └host (8b)┘

Adresa sítě:  192.168.1.0
Broadcast:    192.168.1.255
Hosty:        192.168.1.1 – 192.168.1.254
```

Adresu sítě spočítáš logickým součinem (AND) adresy a masky.

### Převodní tabulka

| Prefix | Maska | Host bitů | Použitelných adres |
| :-- | :-- | :-- | :-- |
| /24 | 255.255.255.0 | 8 | 254 |
| /25 | 255.255.255.128 | 7 | 126 |
| /26 | 255.255.255.192 | 6 | 62 |
| /27 | 255.255.255.224 | 5 | 30 |
| /28 | 255.255.255.240 | 4 | 14 |
| /29 | 255.255.255.248 | 3 | 6 |
| /30 | 255.255.255.252 | 2 | 2 |

Použitelné adresy = 2^(host bitů) − 2 (odečítá se adresa sítě a [[broadcast]]).

### Hodnoty posledního oktetu masky

Maska může v oktetu nabývat jen těchto hodnot (jedničky vždy zleva souvisle):

```
0, 128, 192, 224, 240, 248, 252, 254, 255
```

### K čemu je to prakticky

Podle masky zařízení pozná, jestli je cíl **ve stejné síti** (pošle rámec přímo) nebo **v jiné** (pošle ho na [[default gateway]]).

### Proč se sítě dělí

Menší podsítě = méně [[broadcast|broadcastů]], lepší bezpečnost (oddělení oddělení) a přehlednější správa. Když potřebuješ různě velké podsítě, použiješ [[VLSM]].

**Souvisí:** [[délka prefixu]], [[IPv4]], [[VLSM]], [[IP adresa]], [[default gateway]], [[broadcast]]
