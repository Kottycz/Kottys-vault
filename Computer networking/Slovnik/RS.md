---
aliases: [Router Solicitation]
tags: [slovnik]
---

# RS

**Router Solicitation** – zpráva [[NDP]], kterou se zařízení po připojení k [[IPv6]] síti ptá: "je tu nějaký [[router]]?" Router odpoví zprávou [[RA]].

---

## Podrobně

### Proč existuje

[[RA]] router rozesílá periodicky, ale mezi dvěma oznámeními jsou desítky sekund. Nově připojené zařízení nechce tak dlouho čekat na adresu – proto si RA vyžádá samo.

### Průběh

```
Zařízení                              Router

  RS  →  ff02::2 (všechny routery)
  "je tu router? potřebuju prefix"
  ────────────────────────────────►

  ◄────────────────────────────────
                    RA  →  ff02::1 (všechna zařízení)
                    "jsem tu, prefix je 2001:db8:acad:1::/64"
```

### Adresy ve zprávě

| Pole | Hodnota |
| :-- | :-- |
| Cíl | `ff02::2` – [[multicast]] všech routerů |
| Zdroj | [[LLA]] zařízení, nebo `::` (když ještě nemá adresu) |

### Co následuje

Z prefixu v odpovědi si zařízení složí adresu pomocí [[SLAAC]], ověří ji přes [[DAD]] a nastaví si [[LLA]] routeru jako [[default gateway]].

### Obdoba v IPv4

Zhruba odpovídá DHCP Discover – taky se jím zařízení ptá "je tu někdo, kdo mi dá adresu?". Rozdíl je, že RS se ptá jen routerů (multicast), zatímco DHCP Discover jde [[broadcast|broadcastem]] všem.

**Souvisí:** [[RA]], [[NDP]], [[SLAAC]], [[IPv6]], [[LLA]], [[multicast]]
