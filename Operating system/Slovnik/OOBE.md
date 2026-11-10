---
aliases: [Out-of-Box Experience, bypassnro]
tags: [slovnik]
---

# OOBE

**Out-of-Box Experience** – průvodce prvním spuštěním Windows (jazyk, klávesnice, síť, účet). Např. Windows 11 v OOBE vynucuje Microsoft účet, pokud má internet.

---

## Podrobně

- objeví se po instalaci, než se poprvé dostaneš na plochu
- **Shift + F10** otevře příkazový řádek přímo v OOBE
- `oobe\bypassnro` (*bypass network requirement*) → po restartu nabídne „I don't have internet“ a **lokální účet**
- spolehlivé je navíc odpojit síť (v praxi NIC 1 v CyLabu)
- jméno `Administrator` OOBE nepovolí (je rezervované) → vytvoří se dočasný účet (`temp`) a vestavěný Administrator se zapne až potom (`Enable-LocalUser`)

**Souvisí:** [[00_Priprava_OS]]
