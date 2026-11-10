---
aliases: [Domain Controller, DC, radic domeny]
tags: [slovnik]
---

# Řadič domény

**Domain Controller (DC)** – server, na kterém běží [[AD DS]] a který ověřuje přihlášení do domény. Např. `SRV1-DC` v praxi je řadič domény `kotrba.cyberschool.internal`.

---

## Podrobně

- drží kopii databáze AD (`NTDS`) a sdílené složky **SYSVOL** a **NETLOGON** (politiky a přihlašovací skripty)
- zpravidla je zároveň **[[DNS]] serverem** domény
- server se stane řadičem **povýšením** (`Install-ADDSForest` pro nový les, `Install-ADDSDomainController` pro další DC)
- před povýšením musí mít **finální jméno** a **statickou IP**
- první řadič v lese drží všech 5 rolí [[FSMO]] a je **Global Catalog**
- na řadiči nejsou lokální účty a skupiny – všechno je v AD
- **DSRM heslo** – heslo pro nouzový režim obnovy adresářových služeb, když AD neběží

**Souvisí:** [[01_AD_DS]]
