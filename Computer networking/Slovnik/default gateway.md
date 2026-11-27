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

### Brána na switchi

Switch vrstvy 2 nesměruje, ale potřebuje bránu, aby byl **spravovatelný z jiné sítě** (SSH z PC admina v jiné VLAN):

```
S1(config)# ip default-gateway 192.168.99.1
```

Na data rámce uživatelů to nemá vliv, týká se jen provozu samotného switche.

### Brána na routeru

Router místo brány používá **výchozí cestu** (default route), tzv. gateway of last resort:

```
R1(config)# ip route 0.0.0.0 0.0.0.0 203.0.113.1
```

V `show ip route` je pak označená `S*`.

### Pravidla

- brána musí být **ve stejné podsíti** jako zařízení,
- obvykle se dává první (`.1`) nebo poslední použitelná adresa podsítě,
- když brána vypadne, celá síť ztratí spojení ven. Řeší se to **FHRP** (např. HSRP), kde dva routery sdílí jednu virtuální IP brány.

**Souvisí:** [[router]], [[IP adresa]], [[maska podsítě]], [[DHCP]], [[ARP]]
