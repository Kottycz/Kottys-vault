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

### Užitečné doplňky

| Příkaz | K čemu |
| :-- | :-- |
| `show debugging` | které debugy jsou zapnuté |
| `undebug all` / `no debug all` | vypne všechny debugy najednou |
| `service timestamps debug datetime msec` | ke každé zprávě přidá čas s milisekundami |
| `logging synchronous` (na lince) | debug zprávy nepřeruší rozepsaný příkaz |

### Bezpečný postup

1. nejdřív si připravit `undebug all`, abys ho mohl hned zadat,
2. zapnout co nejužší debug (`debug ip icmp`, ne `debug all`),
3. vyvolat problém (např. ping),
4. přečíst zprávy a debug hned vypnout.

Na zatíženém produkčním routeru může široký debug úplně zahltit CPU a router přestane reagovat.

**Souvisí:** [[IOS]], [[terminal monitor]], [[ICMP]], [[ping]], [[příkazy show]], [[Budovani_male_site]]
