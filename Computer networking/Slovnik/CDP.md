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

### Jak často a kam

- CDP zprávy se posílají každých **60 s** (`cdp timer`),
- soused je v tabulce platný **180 s** (holdtime). Když přestane posílat, po 3 minutách zmizí,
- posílají se na [[multicast]] MAC adresu `01:00:0C:CC:CC:CC`, router je dál nepřeposílá, takže vidíš jen **přímé sousedy**.

### LLDP – otevřená alternativa

**LLDP** (Link Layer Discovery Protocol, [[IEEE]] 802.1AB) dělá to samé co CDP, ale funguje u všech výrobců. Na Cisco je ve výchozím stavu vypnutý:

```
S1(config)# lldp run
S1# show lldp neighbors
```

### Použití při kreslení topologie

Když nemáš schéma sítě, připojíš se na jeden switch, `show cdp neighbors detail` ti ukáže sousedy a jejich IP adresy, připojíš se na ně a pokračuješ. Tak se dá zmapovat celá síť.

**Souvisí:** [[IOS]], [[příkazy show]], [[router]], [[switch]], [[topologie]], [[Budovani_male_site]]
