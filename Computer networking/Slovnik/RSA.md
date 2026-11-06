---
aliases: [RSA klíče, crypto key generate rsa]
tags: [slovnik]
---

# RSA

**RSA** – **asymetrické šifrování** s dvojicí klíčů: **veřejný** (kdokoli ho smí znát) a **soukromý** (zůstává v zařízení). Příklad: switch si vygeneruje RSA pár a veřejný klíč nabídne každému, kdo se připojí přes [[SSH]].

---

## Podrobně

### Proč SSH potřebuje RSA

- Bez RSA klíčů se SSH server **nezapne**.
- Klíče slouží k vyjednání šifrovaného spojení a k ověření identity zařízení.

### Generování na Cisco

Nejdřív musí být nastaven **hostname** a **domain-name**, jinak klíče nejdou vygenerovat.

```
S1(config)# ip domain-name cisco.com
S1(config)# crypto key generate rsa
How many bits in the modulus [512]: 1024
```

- **Modulus** = délka klíče. 1024 b stačí na cvičení, **delší = bezpečnější, ale pomalejší generování**.
- Vygenerování klíče **automaticky zapne SSH**.
- Smazání: `crypto key zeroize rsa` – SSH server se tím vypne.

### SSH verze

Starší IOS defaultně podporují v1 i v2, **v1 má známé slabiny**. Vynutit v2: `ip ssh version 2`.

**Souvisí:** [[SSH]], [[PuTTY]], [[TLS]], [[VTY]], [[IOS]]
