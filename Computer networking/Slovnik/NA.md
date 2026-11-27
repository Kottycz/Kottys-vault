---
aliases: [Neighbor Advertisement]
tags: [slovnik]
---

# NA

**Neighbor Advertisement** – odpověď na [[NS]] ve [[IPv6]] síti. Zařízení jí oznamuje svoji [[MAC adresa|MAC adresu]]. Obdoba ARP Reply.

---

## Podrobně

### Kdy se posílá

- **Jako odpověď na [[NS]]** – "ptal ses na tuhle adresu, tady je moje MAC"
- **Nevyžádaně (unsolicited)** – zařízení samo oznámí změnu, např. po výměně síťové karty nebo při přebírání adresy jiným zařízením

### Příznaky ve zprávě

| Příznak | Význam |
| :-- | :-- |
| **R** (Router) | odesílatel je [[router]] |
| **S** (Solicited) | je to odpověď na konkrétní NS |
| **O** (Override) | příjemce má přepsat starý záznam v cache |

### Role v DAD

Při [[DAD]] je NA **špatná zpráva** – když se zařízení ptá NS na adresu, kterou si chce vzít, a někdo odpoví NA, znamená to, že adresa je už obsazená a nelze ji použít.

### Srovnání s ARP

| | ARP Reply (IPv4) | NA (IPv6) |
| :-- | :-- | :-- |
| Protokol | přímo nad Ethernetem | ICMPv6 / [[NDP]] |
| Nevyžádané oznámení | gratuitous ARP | unsolicited NA |
| Příznaky | ne | R, S, O |

### Bezpečnost

Podobně jako ARP spoofing existuje **NA spoofing** – útočník odpoví "ta adresa jsem já" a odkloní provoz na sebe. Obrana: ND inspection, SEND.

### Adresy ve zprávě

- jako odpověď na NS jde NA **unicastem** přímo tazateli,
- **nevyžádaná** NA (zařízení změnilo MAC adresu nebo oznamuje novou adresu) jde na multicast `FF02::1` všem.

### Příznaky

| Příznak | Význam |
| :-- | :-- |
| R (Router) | odesílatel je router |
| S (Solicited) | odpověď na NS |
| O (Override) | přepiš starý záznam v neighbor cache |

### Ve Wiresharku

NA je zpráva **ICMPv6 typu 136**. Filtr: `icmpv6.type == 136`. Ve zprávě je volba „Target link-layer address" s MAC adresou.

**Souvisí:** [[NS]], [[NDP]], [[DAD]], [[ARP]], [[IPv6]], [[MAC adresa]]
