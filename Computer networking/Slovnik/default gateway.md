---
aliases: [výchozí brána, default gw, brána]
tags: [slovnik]
---

# default gateway

**Výchozí brána** – [[IP adresa]] rozhraní [[router|routeru]], kam zařízení posílá provoz určený **mimo vlastní síť**.

---

## Podrobně

### K čemu slouží

Zařízení podle [[maska podsítě|masky podsítě]] pozná, jestli je cíl ve stejné síti:

- **stejná síť** → pošle rámec přímo cílovému zařízení (MAC zjistí přes [[ARP]])
- **jiná síť** → pošle rámec na MAC adresu výchozí brány, ta ho pošle dál

Bez nastavené brány zařízení komunikuje jen ve své vlastní podsíti – na internet se nedostane.

### Příklad

```
PC1:      192.168.1.10 /24
Brána:    192.168.1.1  (rozhraní routeru)

Cíl 192.168.1.50  → stejná síť → přímo
Cíl 8.8.8.8       → jiná síť   → přes bránu 192.168.1.1
```

Brána musí být **ve stejné podsíti** jako zařízení, jinak ji nelze oslovit.

### Odkud se bere

- automaticky z [[DHCP]] (běžná zařízení)
- ručně při statickém nastavení (servery, [[router|routery]])
- u [[IPv6]] z [[RA]] zprávy od routeru

### Zobrazení

- Windows: `ipconfig` → řádek "Default Gateway"
- Linux: `ip route` → řádek začínající `default via`

### Co se stane při špatném nastavení

Když je brána špatně, [[ping]] uvnitř sítě funguje, ale mimo síť ne – typický příznak chybné konfigurace.

**Souvisí:** [[router]], [[IP adresa]], [[maska podsítě]], [[DHCP]], [[ARP]]
