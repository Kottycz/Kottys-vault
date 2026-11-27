---
aliases: [Content Addressable Memory, tabulka MAC adres, tabulka CAM, MAC address table]
tags: [slovnik]
---

# CAM

**CAM** (Content Addressable Memory) – rychlá paměť v [[switch|přepínači]], kde je uložená **tabulka MAC adres** (která [[MAC adresa]] je na kterém portu). Příklad: PC s MAC `AA:BB:..` je na portu Fa0/3 → rámec pro něj jde jen ven z Fa0/3.

---

## Podrobně

- speciální paměť pro **vysokorychlostní vyhledávání** (hledá se podle obsahu, ne podle adresy),
- proto se tabulce MAC adres říká i **tabulka CAM**,
- jedna hlavní tabulka na switch: rámec s danou cílovou MAC vždy odchází stejným portem,
- učí se ze **zdrojové MAC** příchozích rámců, položka vyprší po **5 minutách** bez provozu (výchozí),
- není-li cíl v tabulce, jde rámec všude kromě příchozího portu ([[neznámý unicast]]).

### Příkazy

| Příkaz | Co dělá |
| :-- | :-- |
| `show mac address-table` | celá tabulka (VLAN, MAC, typ, port) |
| `show mac address-table dynamic` | jen naučené záznamy |
| `show mac address-table interface fa0/1` | MAC adresy na jednom portu |
| `clear mac address-table dynamic` | smaže naučené záznamy |
| `mac address-table aging-time 600` | změní dobu platnosti (výchozí 300 s) |

### Typy záznamů

- **DYNAMIC** – naučené z provozu, po 5 minutách bez provozu zmizí,
- **STATIC** – zadané ručně nebo přes port security, nevyprší.

### Útok MAC flooding

Útočník zahltí switch tisíci falešných zdrojových MAC adres. Tabulka CAM má omezenou velikost, a když se zaplní, switch nové cíle nezná a **rozesílá rámce na všechny porty jako hub**. Útočník pak vidí provoz ostatních. Obrana: **port security** (omezení počtu MAC adres na port).

**Souvisí:** [[switch]], [[MAC adresa]], [[neznámý unicast]], [[Koncepty_prepinani]]
