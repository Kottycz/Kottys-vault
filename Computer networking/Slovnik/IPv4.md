---
aliases: [Internet Protocol version 4]
tags: [slovnik]
---

# IPv4

**Internet Protocol version 4** – protokol síťové vrstvy s **32bitovou** adresou, zapisovanou jako čtyři čísla 0–255 oddělená tečkami (`192.168.1.10`).

---

## Podrobně

### Zápis adresy

Adresa má 32 bitů, rozdělených na 4 oktety po 8 bitech:

```
   192    .   168    .    1     .    10
11000000 . 10101000 . 00000001 . 00001010
```

Každý oktet tedy může být 0–255.

### Síťová a hostitelská část

Adresa se dělí na dvě části podle [[maska podsítě|masky podsítě]]:

```
192.168.1.10 / 24
└──── síť ───┘└host┘

Síťová část:      192.168.1    (stejná pro všechna zařízení v síti)
Hostitelská část: .10          (jedinečná pro každé zařízení)
```

### Speciální adresy v každé síti

| Adresa | Význam |
| :-- | :-- |
| **Adresa sítě** | všechny host bity = 0 (`192.168.1.0`) |
| **Broadcast** | všechny host bity = 1 (`192.168.1.255`) |
| **Použitelné hosty** | vše mezi tím (`.1` až `.254`) |

Počet použitelných adres = 2^(počet host bitů) − 2

### Privátní rozsahy

Nejsou směrovatelné na internetu, používají se v lokálních sítích (překládá je [[NAT]]):

| Rozsah | Maska |
| :-- | :-- |
| 10.0.0.0 – 10.255.255.255 | /8 |
| 172.16.0.0 – 172.31.255.255 | /12 |
| 192.168.0.0 – 192.168.255.255 | /16 |

### Další speciální adresy

- `127.0.0.1` – **loopback** (sám sobě, "localhost")
- `169.254.x.x` – **APIPA** (když selže [[DHCP]])
- `255.255.255.255` – broadcast do celé sítě

### Vyčerpání adres

32 bitů = asi 4,3 miliardy adres, což už nestačí. Řeší se [[NAT|NATem]] a přechodem na [[IPv6]].

**Souvisí:** [[IP adresa]], [[maska podsítě]], [[délka prefixu]], [[NAT]], [[IPv6]], [[VLSM]], [[broadcast]]
