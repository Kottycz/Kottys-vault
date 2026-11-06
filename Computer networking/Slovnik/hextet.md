---
aliases: [hextety]
tags: [slovnik]
---

# hextet

**Skupina 16 bitů** (čtyři hexadecimální znaky) v [[IPv6]] adrese. Adresa se skládá z **osmi** hextetů oddělených dvojtečkami.

---

## Podrobně

### Umístění

```
2001 : 0db8 : acad : 0001 : 0000 : 0000 : 0000 : 0100
  1      2      3      4      5      6      7      8
└──────── 8 hextetů × 16 bitů = 128 bitů ────────────┘
```

Obdoba oktetu u [[IPv4]] – tam je adresa rozdělená na 4 oktety po 8 bitech.

### Pravidla zkracování

**1) Vynechání úvodních nul v hextetu**

```
0db8  →  db8
0000  →  0
0100  →  100
```

Nuly uvnitř nebo na konci hextetu se **nevynechávají** (`0100` ≠ `01`).

**2) Dvojitá dvojtečka `::`**

Jednu souvislou skupinu nulových hextetů lze nahradit `::`:

```
2001:db8:acad:1:0:0:0:100
2001:db8:acad:1::100
```

**Pozor: `::` smí být v adrese jen jednou!** Jinak by nešlo poznat, kolik nul kde doplnit:

```
2001:0:0:1:0:0:0:100

✓ 2001:0:0:1::100      (zkrácena delší skupina)
✗ 2001::1::100         (nejednoznačné – NEPLATNÉ)
```

### Příklady

| Plný zápis | Zkrácený |
| :-- | :-- |
| `2001:0db8:0000:0000:0000:0000:0000:0001` | `2001:db8::1` |
| `fe80:0000:0000:0000:0204:61ff:fe9d:f156` | `fe80::204:61ff:fe9d:f156` |
| `0000:0000:0000:0000:0000:0000:0000:0001` | `::1` (loopback) |
| `0000:0000:0000:0000:0000:0000:0000:0000` | `::` (neurčená) |

**Souvisí:** [[IPv6]], [[délka prefixu]], [[GUA]], [[LLA]], [[EUI-64]]
