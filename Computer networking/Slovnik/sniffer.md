---
aliases: [packet sniffer, čichač paketů, odposlech]
tags: [slovnik]
---

# sniffer

**Čichač paketů** – nástroj/software, který odposlouchává a zaznamenává síťový provoz procházející sítí.

---

## Podrobně

### Legitimní vs. škodlivé použití

Sniffer sám o sobě není útok – síťoví administrátoři ho běžně používají k diagnostice problémů (např. Wireshark). Stává se útokem, když ho použije někdo neoprávněný k odposlechu cizího provozu (hesla, citlivá data).

### Proč funguje

Na nešifrovaných protokolech (starý [[HTTP|HTTP]], [[Telnet]]) sniffer uvidí data v čitelné podobě. Na přepínané síti ([[switch]]) funguje jen omezeně – útočník potřebuje provoz na svůj port nějak nasměrovat (např. [[ARP]] spoofing).

### Obrana

Šifrování ([[HTTPS]], [[SSH]]) – i odposlechnutá data jsou pak nečitelná.

### Promiskuitní režim

Normálně [[NIC|síťová karta]] přijme jen rámce pro svou MAC adresu, broadcast a multicast. Sniffer kartu přepne do **promiskuitního režimu**, kdy přijme všechno, co na ni dorazí.

### Na switchi to nestačí

Switch posílá rámce jen na port cíle, takže sniffer na běžném portu vidí jen vlastní provoz. Možnosti:

- **SPAN / port mirroring** – switch kopíruje provoz z vybraných portů na port se snifferem (legitimní diagnostika),
- **útok** – MAC flooding nebo [[ARP]] spoofing, aby provoz šel přes útočníka.

### Nastavení SPAN na Cisco

```
S1(config)# monitor session 1 source interface fa0/1
S1(config)# monitor session 1 destination interface fa0/24
```

Na port Fa0/24 se připojí PC s [[Wireshark|Wiresharkem]].

**Souvisí:** [[brute force]], [[MITM]], [[ARP]]
