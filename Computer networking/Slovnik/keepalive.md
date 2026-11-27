---
aliases: [keepalives, line protocol]
tags: [slovnik]
---

# keepalive

**Keepalive** – malé pravidelné zprávy, kterými si zařízení na lince ověřují, že druhá strana **žije**. Příklad: na Ethernetu rozhraní v `show interfaces` ukazuje `Keepalive set (10 sec)`.

---

## Podrobně

### Dva stavy rozhraní

```
FastEthernet0/18 is up, line protocol is up (connected)
```

| Část | Vrstva | Význam |
| :-- | :-- | :-- |
| **is up** | fyzická | přichází nosný signál (carrier detect) |
| **line protocol is up** | linková | přicházejí **keepalive** zprávy |

### Kombinace a diagnostika

| Stav | Příčina |
| :-- | :-- |
| up / **down** | nesoulad enkapsulace, druhá strana error-disabled, hardwarový problém |
| **down / down** | kabel nezapojen, jiný problém rozhraní, druhá strana vypnutá |
| **administratively down** | rozhraní ručně vypnuto příkazem `shutdown` |

### Kde keepalive potkáš

| Kde | K čemu |
| :-- | :-- |
| rozhraní routeru (Ethernet, sériové linky) | ověření, že linka funguje, výchozí interval 10 s |
| [[TCP]] keepalive | ověření, že druhá strana spojení ještě žije, i když se dlouho neposílají data |
| [[OSPF]], [[EIGRP]] Hello | sousedé si dávají vědět, že žijí |

### V show interfaces

```
R1# show interfaces g0/0/0
  Keepalive set (10 sec)
```

Když na sériové lince keepalive nepřichází, line protocol spadne na **down** i při fyzicky zapojeném kabelu.

**Souvisí:** [[příkazy show]], [[Ethernet]], [[IOS]], [[kolize]]
