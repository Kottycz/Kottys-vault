---
aliases: [Cisco Discovery Protocol, show cdp neighbor, no cdp run, no cdp enable]
tags: [slovnik]
---

# CDP

**Cisco Discovery Protocol** – proprietární protokol Cisco na **vrstvě datového spojení**, kterým si sousední zařízení Cisco navzájem zjistí, kdo je kdo.

```
show cdp neighbor
```

---

## Podrobně

### Co dělá

Protože CDP pracuje na **vrstvě datového spojení** (2), mohou se dvě nebo více síťových zařízení Cisco – například [[router|směrovače]] – o sobě **dozvědět, i když nebylo navázáno připojení na 3. vrstvě**. K tomu nepotřebují ani [[IP adresa|IP adresy]].

Podporuje i zařízení s různými protokoly síťové vrstvy.

### Proprietární

Je to protokol **jen od Cisco**. Nestandardní zařízení jiných výrobců mu nerozumí. Univerzální obdoba je **LLDP**.

### Zobrazení sousedů

```
show cdp neighbor
```

Vypíše přímo připojená zařízení – jejich název, typ, kterým rozhraním jsou připojena a které rozhraní používá soused. Hodí se při zjišťování topologie sítě, když nemáš dokumentaci.

### Vypnutí

| Rozsah | Příkaz | Režim |
| :-- | :-- | :-- |
| **globálně** | `no cdp run` | globální konfigurace |
| **na rozhraní** | `no cdp enable` | konfigurace rozhraní |

### Bezpečnost

CDP je ve výchozím stavu zapnuté a prozrazuje informace o zařízení (typ, verze IOS, adresy), proto se na rozhraních směřujících ven často vypíná.

**Souvisí:** [[IOS]], [[příkazy show]], [[router]], [[switch]], [[topologie]], [[Budovani_male_site]]
