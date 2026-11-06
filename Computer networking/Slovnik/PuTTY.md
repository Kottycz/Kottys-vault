---
aliases: [putty]
tags: [slovnik]
---

# PuTTY

**PuTTY** – bezplatný **terminálový klient** pro připojení k zařízení přes [[SSH]], [[Telnet]] nebo sériovou linku (console). Příklad: v PuTTY zadáš `172.17.99.11`, port `22`, typ SSH → klikneš Open → přihlásíš se do switche.

---

## Podrobně

### Typy spojení

| Typ | Použití |
| :-- | :-- |
| **SSH** | šifrované vzdálené spojení, port **22** |
| **Telnet** | nešifrované, port **23**, jen laboratoř |
| **Serial** | kabel do console portu (rychlost obvykle 9600) |

### Postup připojení přes SSH

1. Host Name = IP adresa [[SVI]] switche (např. `172.17.99.11`).
2. Port **22**, Connection type **SSH**.
3. Open → přihlášení (`admin` / heslo z `username admin secret ...`).
4. Přejít do privilegovaného režimu: `enable`.

### Poznámky

- PC musí být ve stejné síti nebo mít cestu přes [[default gateway]].
- Prvně se zobrazí varování o hostitelském klíči ([[RSA]]) – při prvním připojení je to normální.

**Souvisí:** [[SSH]], [[Telnet]], [[VTY]], [[RSA]], [[SVI]]
