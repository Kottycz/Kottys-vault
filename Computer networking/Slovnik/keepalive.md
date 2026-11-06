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

**Souvisí:** [[příkazy show]], [[Ethernet]], [[IOS]], [[kolize]]
