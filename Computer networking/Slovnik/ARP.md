---
aliases: [Address Resolution Protocol]
tags: [slovnik]
---

# ARP

**Address Resolution Protocol** – zjišťuje [[MAC adresa|MAC adresu]] k známé [[IPv4]] adrese v lokální síti. Bez něj by rámec nevěděl, komu se má na [[switch|switchi]] doručit.

---

## Podrobně

### Proč je potřeba

Když chce počítač poslat data, zná cílovou **IP adresu** (vrstva 3, [[Sitova_vrstva|síťová]]). Aby ale mohl sestavit [[Ethernet|ethernetový]] rámec a poslat ho po [[LAN]], potřebuje cílovou **MAC adresu** (vrstva 2, [[Data_link|linková]]). ARP tenhle překlad zajišťuje. Funguje jen **uvnitř jedné sítě** (jedné [[broadcast doména|broadcast domény]]), přes [[router]] neprojde.

### Jak funguje

```
PC1 chce poslat data na 192.168.1.9, ale nezná jeho MAC.

1. ARP Request  → broadcast na celou síť
   "Kdo má 192.168.1.9? Odpověz PC1."
   (cílová MAC = FF:FF:FF:FF:FF:FF)

2. ARP Reply    → unicast zpátky jen PC1
   "192.168.1.9 jsem já, moje MAC je 00:1A:2B:3C:4D:5E."

3. PC1 si dvojici uloží do ARP cache a pošle data.
```

- Request jde [[broadcast|broadcastem]] (slyší ho všichni v síti, ale odpoví jen ten, komu IP patří).
- Reply jde [[unicast|unicastem]] (jen tazateli).
- Cíl si při tom zároveň uloží MAC tazatele, takže se už nemusí ptát zpátky.

### Co je v ARP zprávě

ARP se vkládá přímo do ethernetového rámce, [[EtherType]] = `0x0806`.

| Pole | Request | Reply |
| :-- | :-- | :-- |
| Operation | 1 | 2 |
| Sender MAC | MAC PC1 | MAC cíle |
| Sender IP | IP PC1 | IP cíle |
| Target MAC | 00:00:00:00:00:00 (neznám) | MAC PC1 |
| Target IP | hledaná IP | IP PC1 |

### ARP cache (tabulka)

Naučené dvojice IP ↔ MAC se ukládají do **ARP tabulky**, aby se zařízení neptalo pokaždé znovu.

- **dynamické záznamy** – naučené přes ARP, po čase vyprší (Windows a Linux v řádu desítek sekund až minut, Cisco router **4 hodiny**),
- **statické záznamy** – zadané ručně, nevyprší (Windows `arp -s`).

| Zařízení | Zobrazit | Smazat |
| :-- | :-- | :-- |
| Windows | `arp -a` | `arp -d` |
| Linux | `ip neigh` | `ip neigh flush all` |
| Cisco | `show ip arp` | `clear arp-cache` |

### První ping na Cisco ztratí paket

Typická věc z labů: první `ping` z routeru vypadá `.!!!!` (úspěšnost 80 %). První paket se ztratí, protože router teprve čeká na ARP odpověď. Není to chyba sítě.

### Komunikace mimo vlastní síť

Když je cíl v jiné síti (zařízení to pozná podle [[maska podsítě|masky]]), ARP se **neptá na cílovou IP**, ale na MAC adresu [[default gateway|výchozí brány]]. Rámec pak jde na [[router]], ten ho rozbalí a pro další síť si udělá vlastní ARP. MAC adresy se tedy mění na každém skoku ([[hop]]), IP adresy zůstávají stejné.

### Zvláštní typy ARP

- **Gratuitous ARP** – zařízení oznámí svou IP a MAC samo od sebe, bez otázky. Používá se po startu nebo po změně IP, ostatní si aktualizují tabulku. Zároveň odhalí duplicitní IP v síti.
- **Proxy ARP** – router odpoví na ARP za zařízení v jiné síti a podstrčí svou MAC. Dnes se moc nepoužívá.

### Problémy s ARP

- **Broadcasty** – ve velké síti se spousta zařízení ptá zároveň a broadcast zatěžuje všechny. Řeší se rozdělením sítě na menší ([[VLAN]], podsítě).
- **ARP spoofing / poisoning** – ARP nemá ověřování, kdokoliv může odpovědět „ta IP jsem já". Útočník tak nasměruje provoz na sebe ([[MITM|man-in-the-middle]]) a může ho odposlouchávat. Obrana: **Dynamic ARP Inspection (DAI)** na switchi, statické záznamy u důležitých zařízení, monitorování.

### U IPv6

[[IPv6]] ARP vůbec nepoužívá. Stejnou úlohu tam plní [[NDP]] (Neighbor Discovery Protocol) pomocí zpráv [[NS]] (Neighbor Solicitation) a [[NA]] (Neighbor Advertisement). Místo broadcastu používá [[multicast]], takže neruší všechna zařízení.

**Souvisí:** [[MAC adresa]], [[IP adresa]], [[broadcast]], [[default gateway]], [[NDP]], [[EtherType]], [[MITM]], [[Rozliseni_adres]]
