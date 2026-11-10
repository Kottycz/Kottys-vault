---
aliases: [Active Directory Domain Services, doména Windows]
tags: [slovnik]
---

# AD DS

**Active Directory Domain Services** – role Windows Serveru, která centrálně spravuje uživatele, počítače, skupiny a oprávnění v doméně. Např. v doméně `kotrba.cyberschool.internal` se jedním účtem přihlásíš na kterýkoli počítač v doméně.

---

## Podrobně

### Struktura

- **les (forest)** – nejvyšší úroveň, sdílí jedno schéma; první doména v něm je kořenová
- **doména** – skupina objektů se společnou databází a pravidly (např. `kotrba.cyberschool.internal`, NetBIOS `KOTRBA`)
- **OU (organizační jednotka)** – složka v doméně pro třídění objektů a nastavování politik
- **objekty** – uživatelé, počítače, skupiny

### Jak funguje

- databáze je uložená na **[[řadič domény|řadičích domény]]** a mezi nimi se replikuje
- komunikuje přes [[LDAP]], ověřuje přes **Kerberos** (vyžaduje synchronizovaný čas)
- bez [[DNS]] nefunguje – klienti hledají řadič přes DNS záznamy
- instalace: `Install-WindowsFeature AD-Domain-Services`, povýšení: `Install-ADDSForest`
- grafická správa: **ADUC** (`dsa.msc`)

**Souvisí:** [[FSMO]], [[01_AD_DS]]
