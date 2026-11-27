---
aliases: [přepínač, switche]
tags: [slovnik]
---

# switch

**Přepínač** – zařízení spojové vrstvy (OSI 2), které propojuje zařízení **v jedné síti** a přeposílá rámce podle [[MAC adresa|MAC adres]].

---

## Podrobně

### Jak se učí

Switch si buduje **MAC tabulku** (CAM tabulku):

```
1. Přijde rámec na port 3 se zdrojovou MAC 00:1A:2B:...
   → switch si zapíše: 00:1A:2B:... = port 3

2. Chce poslat rámec na cílovou MAC:
   - zná ji     → pošle jen na příslušný port (unicast)
   - nezná ji   → pošle na všechny porty kromě příchozího (flooding)
   - broadcast  → pošle na všechny porty kromě příchozího
```

Záznamy po čase vyprší (typicky 5 minut).

Zobrazení: `show mac address-table` (Cisco)

### Switch vs. hub

Starý **hub** posílal všechno všem porty – vznikaly kolize a provoz viděl každý. Switch posílá rámec jen tam, kam patří:

- každý port = vlastní **kolizní doména** (proto může jet [[full-duplex]], bez kolizí)
- všechny porty = jedna **broadcastová doména** (broadcast rozdělí až [[router]])

### Metody přepínání

- **Store-and-forward** – načte celý rámec, ověří [[FCS]], pak pošle dál (bezpečnější, výchozí u Cisco)
- **Cut-through** – přečte jen cílovou MAC a hned začne posílat (rychlejší, ale propouští i vadné rámce)

### VLAN

Switch umí logicky rozdělit porty do **VLAN** – oddělených virtuálních sítí, které se navzájem nevidí, přestože jsou na jednom fyzickém switchi. Aby spolu VLANy komunikovaly, je potřeba [[router]] (nebo L3 switch).

Pro správu switche přes IP se nastavuje virtuální rozhraní [[SVI]].

### Typy switchů

| Typ | Vlastnosti |
| :-- | :-- |
| nespravovaný | bez konfigurace, jen přeposílá rámce, domácnost |
| spravovaný | VLAN, STP, port security, SSH, firmy |
| [[přepínač vrstvy 3]] | navíc směruje mezi VLAN |
| PoE switch | napájí telefony, AP, kamery ([[PoE]]) |

### Výchozí stav Cisco switche

- všechny porty jsou zapnuté a ve VLAN 1,
- žádná IP adresa (aby byl spravovatelný, potřebuje [[SVI]]),
- auto rychlost a duplex,
- STP zapnutý.

Proto Cisco switch po vybalení hned funguje jako obyčejný switch.

### Základní zabezpečení

```
S1(config)# hostname S1
S1(config)# enable secret Cisco123
S1(config)# interface range fa0/10 - 24
S1(config-if-range)# shutdown
S1(config)# interface fa0/1
S1(config-if)# switchport port-security
S1(config-if)# switchport port-security maximum 2
```

Nepoužívané porty vypnout, na portech k uživatelům **port security** (omezení počtu MAC adres).

**Souvisí:** [[router]], [[MAC adresa]], [[FCS]], [[full-duplex]], [[broadcast]], [[SVI]], [[CSMA-CD]]
