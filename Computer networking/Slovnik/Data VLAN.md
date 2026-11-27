---
aliases: [uživatelská VLAN, user VLAN]
tags: [slovnik]
---

# Data VLAN

**Data VLAN** – [[VLAN]] určená pro běžný provoz uživatelů a jejich zařízení (počítače, servery). Příklad: VLAN 10 pro kanceláře, VLAN 20 pro výrobu.

---

## Podrobně

- přenáší data vytvářená uživateli, ne řídicí provoz ani hlas,
- provoz pro správu ([[Management VLAN]]) a hlas ([[Voice VLAN]]) se od ní odděluje,
- používá se pro rozdělení sítě podle oddělení, typu uživatelů nebo zařízení,
- port patří do jedné data VLAN, nastavuje se jako access port.

### Konfigurace

```
S1(config)# vlan 10
S1(config-vlan)# name Kancelare
S1(config-vlan)# exit
S1(config)# interface range fa0/1 - 10
S1(config-if-range)# switchport mode access
S1(config-if-range)# switchport access vlan 10
```

Ověření: `show vlan brief`.

### Návrh: VLAN a podsítě

Každá data VLAN má vlastní IP podsíť. Je přehledné, když číslo VLAN odpovídá třetímu oktetu:

| VLAN | Název | Podsíť |
| :-- | :-- | :-- |
| 10 | Kancelare | 192.168.10.0/24 |
| 20 | Vyroba | 192.168.20.0/24 |
| 30 | Hoste | 192.168.30.0/24 |

### Komunikace mezi data VLAN

Zařízení z různých data VLAN spolu bez routeru nemluví. Potřebuješ [[Inter-VLAN routing]] (router nebo [[přepínač vrstvy 3]]).

**Souvisí:** [[VLAN]], [[Default VLAN]], [[Management VLAN]], [[Voice VLAN]]
