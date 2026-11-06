# [Jak se pozná, že už to mám?]

> Verze: 2026-10-03

### 1. Server je nainstalovaný a dostupný v síti
Přímo na konzoli SRV1-DC (tento krok ještě nejde ověřit z PC1-WIN, protože klient do domény zatím nevstoupil) se úspěšně přihlásíte jako `Administrator` / `Pa55w.rd`. Příkaz `ipconfig` na SRV1-DC ukazuje statickou IP `192.168.200.10/24`.

### 2. AD DS role je nainstalovaná
V **Server Manageru** na Dashboardu vidíte v seznamu rolí položku **AD DS** a **DNS** (obě zelené, bez chyb).

> 📷 **Screenshot sem:** [Server Manager — Dashboard se zelenými rolemi AD DS a DNS]

### 3. Server je řadičem domény
V **Server Manager → Local Server** je u položky *Domain* uvedeno `prijmeni.cyberschool.internal` (ne `WORKGROUP`).

> 📷 **Screenshot sem:** [Server Manager — Local Server, položka Domain s hodnotou prijmeni.cyberschool.internal]

### 4. SRV1-DC drží role FSMO a je Global Catalog
Příkaz `netdom query fsmo` na SRV1-DC vypíše u všech pěti rolí (Schema master, Domain naming master, PDC, RID pool manager, Infrastructure master) server `SRV1-DC.prijmeni.cyberschool.internal`. `Get-ADDomainController -Identity SRV1-DC` ukazuje `IsGlobalCatalog : True`.

> 📷 **Screenshot sem:** [Výstup netdom query fsmo — všech pět rolí na SRV1-DC]

### 5. Nástroje pro správu domény fungují
V **Server Manager → Tools** je dostupná položka **Active Directory Users and Computers** a po jejím otevření vidíte strukturu domény `prijmeni.cyberschool.internal` (výchozí kontejnery `Users`, `Computers`, `Domain Controllers`).

> 📷 **Screenshot sem:** [ADUC — otevřená struktura domény prijmeni.cyberschool.internal s výchozími kontejnery]

### 6. Restart nic nerozbije
Po restartu serveru SRV1-DC proběhne přihlášení bez chyby jako `PRIJMENI\Administrator`, např. `NOVAK\Administrator` (nikoliv jako lokální účet) a všechny role v Server Manageru zůstávají funkční (žádné červené varování).
