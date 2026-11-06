---
aliases: [debug ip icmp, ladění, příkaz ladění, undebug]
tags: [slovnik]
---

# debug

**Příkaz Cisco [[IOS]], který v reálném čase zobrazuje zprávy o dění v zařízení** (procesech, protokolech, událostech) – nástroj pro ladění a hledání chyb.

```
debug ip icmp
```

---

## Podrobně

### K čemu je

Procesy, protokoly, mechanismy a události operačního systému **generují zprávy**, které sdělují jejich stav. Tyto zprávy mohou poskytnout cenné informace při řešení problémů nebo ověřování systémových operací. Příkaz debug je zobrazí administrátorovi **v reálném čase** pro účely analýzy. Je to velmi důležitý nástroj pro monitorování událostí na zařízení Cisco IOS.

### Příklady z učiva

| Příkaz | Co dělá |
| :-- | :-- |
| `debug ip icmp` | sleduje zprávy [[ICMP]] v routeru (třeba [[echo request]] a echo reply z pingu) |
| `debug ?` | vypíše **stručný popis všech možností** ladicího příkazu |

### Kde se zprávy zobrazí

Některé zprávy systému IOS se automaticky zobrazují při připojení **ke konzoli**, ale **ne při vzdáleném připojení**. Například ladicí výstup se ve výchozím nastavení zobrazuje při připojení ke konzoli. Při vzdáleném připojení (SSH, Telnet) se zapíná příkazem [[terminal monitor]].

### Postup

```
Router# debug ip icmp
(na jiném zařízení: ping na tenhle router)
Router# 
ICMP: echo reply sent, src ..., dst ...
```

### Pozor – debug zatěžuje zařízení

Ladění produkuje spoustu výstupu a může **zpomalit nebo zahltit** router. Používá se krátce a pak se vypne:

```
no debug all
```

nebo `undebug all`.

**Souvisí:** [[IOS]], [[terminal monitor]], [[ICMP]], [[ping]], [[příkazy show]], [[Budovani_male_site]]
