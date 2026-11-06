---
aliases: [Extended Unique Identifier 64]
tags: [slovnik]
---

# EUI-64

**Extended Unique Identifier** – metoda, jak z 48bitové [[MAC adresa|MAC adresy]] vytvořit 64bitové **ID rozhraní** pro [[IPv6]] adresu.

---

## Podrobně

### Postup – tři kroky

```
MAC adresa:        00:1A:2B : 3C:4D:5E

1) Rozdělit na půl a vložit doprostřed FFFE:
                   00:1A:2B : FF:FE : 3C:4D:5E

2) Překlopit 7. bit zleva (U/L bit):
   00 = 0000 0000  →  0000 0010 = 02

3) Výsledek:       021A:2BFF:FE3C:4D5E
```

Spojením s prefixem vznikne celá adresa:

```
2001:db8:acad:1 : 021a:2bff:fe3c:4d5e
└── prefix /64 ──┘ └── ID rozhraní ──┘
```

### Proč se překlápí U/L bit

Bit **U/L** (Universal/Local) v MAC adrese znamená 0 = globálně unikátní (od výrobce). V EUI-64 se význam obrací – proto se překlopí na 1. Prakticky to poznáš tak, že MAC začínající `00` dá ID začínající `02`.

### Jak poznat EUI-64 adresu

Má uprostřed charakteristické **`ff:fe`**:

```
fe80::021a:2bff:fe3c:4d5e
              └──┘
```

### Problém se soukromím

Protože je ID odvozeno z MAC adresy, **adresa zařízení se nemění, i když se přepojí do jiné sítě** – jde ho tak celosvětově sledovat. Z posledních bitů navíc jde vyčíst výrobce ([[OUI]]).

Proto se dnes místo EUI-64 běžně používají **náhodně generovaná ID** (privacy extensions), která se navíc čas od času mění. EUI-64 se ale pořád učí a používá u síťových prvků.

**Souvisí:** [[MAC adresa]], [[IPv6]], [[SLAAC]], [[LLA]], [[OUI]], [[hextet]]
