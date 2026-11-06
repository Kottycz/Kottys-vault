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

**Souvisí:** [[brute force]], [[MITM]], [[ARP]]
