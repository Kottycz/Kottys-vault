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

### Připojení přes konzoli

1. kabel: konzolový (modrý, RJ-45 na DB-9) nebo USB konzole,
2. ve Windows ve Správci zařízení zjistit číslo portu (COM3, COM4),
3. v PuTTY zvolit **Serial**, zadat COM port,
4. rychlost **9600** baudů (8 datových bitů, bez parity, 1 stop bit, bez řízení toku).

### Ukládání relací

V PuTTY si uložíš nastavení pod jménem (Saved Sessions) a příště jen kliknout. Logování výstupu do souboru: Session → Logging → All session output. Hodí se, když potřebuješ výpis z přístroje do protokolu.

### Alternativy

Tera Term, SecureCRT, na Linuxu a macOS `ssh` a `screen` přímo z terminálu, ve Windows 10/11 je `ssh` v příkazovém řádku také.

**Souvisí:** [[SSH]], [[Telnet]], [[VTY]], [[RSA]], [[SVI]]
