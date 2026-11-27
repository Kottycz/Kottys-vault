---
tags: [slovnik]
---

# Telnet

**Protokol pro vzdálené připojení k příkazové řádce zařízení.** Port **23**, nad [[TCP]]. Posílá všechno **nešifrovaně** – dnes se nahrazuje [[SSH]].

---

## Podrobně

### Proč se nepoužívá

Telnet přenáší data v čitelné podobě – **včetně jména a hesla**. Kdokoliv, kdo odposlouchává provoz (Wireshark na sdílené síti), je rovnou přečte.

```
Telnet:  admin / Pa55w.rd    ← čitelné v každém paketu
SSH:     8f3a9c2b1e...       ← zašifrované
```

### Kde ho ještě potkáš

- **Laboratoře a Packet Tracer** – kvůli jednoduchosti, není potřeba generovat klíče
- **Starý hardware**, který SSH neumí
- **Testování otevřených portů**: `telnet server 80` ověří, jestli na portu něco naslouchá (i když protokol není Telnet)

### Konfigurace na Cisco

```
Router(config)# line vty 0 4
Router(config-line)# password heslo
Router(config-line)# login
Router(config-line)# transport input telnet
```

Pro SSH se místo toho použije `transport input ssh` (a je potřeba vygenerovat klíče).

### Doporučení

V reálné síti Telnet **vždy vypnout** a povolit jen SSH:

```
Router(config-line)# transport input ssh
```

### Ukázka, proč je nebezpečný

Ve [[Wireshark|Wiresharku]] stačí na zachyceném Telnet provozu dát „Follow TCP Stream" a vidíš jméno i heslo v čitelné podobě, včetně všech příkazů. U [[SSH]] je tam jen šifrovaný nesmysl.

### Telnet jako testovací nástroj

Telnet klient se dá použít k ověření, jestli je na serveru otevřený [[port]]:

```
C:\> telnet mail.skola.cz 25
220 mail.skola.cz ESMTP
```

Když se připojí, port je otevřený a služba běží. Dnes se k tomu spíš používá `Test-NetConnection server -Port 25` (PowerShell).

### Vypnutí Telnetu na Cisco

```
R1(config)# line vty 0 4
R1(config-line)# transport input ssh
```

Tím se na VTY linkách povolí jen SSH, Telnet se odmítne.

**Souvisí:** [[SSH]], [[TCP]], [[port]], [[running-config]]
