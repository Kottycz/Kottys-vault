---
aliases: [man-in-the-middle, muž uprostřed]
tags: [slovnik]
---

# MITM

**Man-in-the-middle** – útočník se nachází mezi dvěma legitimními entitami (např. klientem a serverem), aby mohl číst nebo upravovat data, která si mezi sebou posílají.

---

## Podrobně

### Jak funguje

```
Klient ──── MITM (útočník) ──── Server
```

Obě strany si myslí, že komunikují přímo spolu – ve skutečnosti jde všechen provoz přes útočníka, který ho může odposlouchávat nebo měnit.

### Kde se s tím setkáš

- Nezabezpečená veřejná Wi-Fi
- [[ARP]] spoofing v lokální síti
- Podvržené [[DNS]] odpovědi

### Obrana

Šifrovaná komunikace ([[HTTPS]], [[TLS]]) – i když útočník data vidí, nemůže je přečíst ani nepozorovaně změnit.

**Souvisí:** [[ARP]], [[HTTPS]], [[TLS]], [[DoS-DDoS]]
