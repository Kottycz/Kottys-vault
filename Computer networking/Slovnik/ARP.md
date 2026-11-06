---
aliases: [Address Resolution Protocol]
tags: [slovnik]
---

# ARP

**Address Resolution Protocol** – zjišťuje [[MAC adresa|MAC adresu]] k známé [[IPv4]] adrese v lokální síti. Bez něj by rámec nevěděl, komu se má na [[switch|switchi]] doručit.

---

## Podrobně

### Proč je potřeba

Když chce počítač poslat data, zná cílovou **IP adresu** (vrstva 3). Aby ale mohl sestavit rámec a poslat ho po [[LAN]], potřebuje cílovou **MAC adresu** (vrstva 2). ARP tenhle překlad zajišťuje.

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

Request jde [[broadcast|broadcastem]] (slyší ho všichni), odpověď jde [[unicast|unicastem]] (jen tazateli).

### ARP cache (tabulka)

Naučené dvojice IP ↔ MAC se ukládají do **ARP tabulky**, aby se počítač neptal pokaždé znovu. Záznamy po čase vyprší.

Zobrazení: `arp -a` (Windows), `ip neigh` (Linux)

### Komunikace mimo vlastní síť

Když je cíl v jiné síti, ARP se **neptá na cílovou IP**, ale na MAC adresu [[default gateway|výchozí brány]]. Rámec pak putuje na [[router]], který ho pošle dál.

### Bezpečnost – ARP spoofing

ARP nemá žádné ověřování – kdokoliv může odpovědět "ta IP jsem já". Útočník tak může nasměrovat provoz na sebe (**man-in-the-middle**). Obrana: Dynamic ARP Inspection, statické záznamy, monitorování.

### U IPv6

[[IPv6]] ARP vůbec nepoužívá – stejnou úlohu tam plní [[NDP]] (Neighbor Discovery Protocol) pomocí zpráv [[NS]] a NA.

**Souvisí:** [[MAC adresa]], [[IP adresa]], [[broadcast]], [[default gateway]], [[NDP]]
