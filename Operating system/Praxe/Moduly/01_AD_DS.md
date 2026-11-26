---
aliases: [Modul 01, Active Directory Domain Services, M01]
---

# Modul 01 – Active Directory Domain Services

Ze **SRV1-DC** se udělá **[[řadič domény]]** a vznikne doména **`kotrba.cyberschool.internal`** (NetBIOS jméno `KOTRBA`). Dělá se jen na SRV1-DC.

> [!info] Proč doména
> Bez domény má každý počítač vlastní uživatele a hesla. Doména ([[AD DS]]) drží uživatele, počítače a oprávnění **centrálně** na řadiči → přihlásíš se stejným účtem na jakémkoli počítači v doméně. Základ je protokol [[LDAP]].

Předchozí: [[00_Priprava_OS|Modul 00]]

---

## 1. Kontrola předpokladů

Před povýšením musí být hotové **jméno** a **statická IP** – po povýšení se mění špatně (jméno je zapsané v AD i DNS).

| Parametr | Hodnota |
| :-- | :-- |
| Hostname | `SRV1-DC` |
| Rozhraní | `Ethernet1` (NIC 2, zapnutá v CyLabu) |
| IPv4 | `192.168.16.10/24` |
| Brána | `192.168.16.1` |
| Účet | `Administrator` / `Pa55w.rd` |

```powershell
hostname
Get-NetIPAddress -InterfaceAlias Ethernet1 -AddressFamily IPv4 | Select-Object IPAddress, PrefixLength
```

---

## 2. Instalace role AD DS

```powershell
Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools
```
- nainstaluje jen **soubory role**, server ještě řadičem není
- `-IncludeManagementTools` přidá **RSAT** = nástroje na správu (ADUC, PowerShell modul ActiveDirectory)

**Kontrola:**
```powershell
Get-WindowsFeature -Name AD-Domain-Services, RSAT-ADDS | Select-Object Name, InstallState
# obojí Installed
```

---

## 3. Povýšení na řadič domény (nový les)

```powershell
$DomainName = "kotrba.cyberschool.internal"
$SecurePassword = ConvertTo-SecureString "Pa55w.rd" -AsPlainText -Force

Install-ADDSForest -DomainName $DomainName -SafeModeAdministratorPassword $SecurePassword -InstallDns:$true -Force:$true
```
- **les (forest)** = nejvyšší úroveň AD; první doména v něm je kořenová → proto `Install-ADDSForest`
- `-SafeModeAdministratorPassword` = **DSRM heslo** – na obnovu AD v nouzovém režimu, když AD neběží
- `-InstallDns:$true` → doinstaluje **DNS server**; AD bez DNS nefunguje (klienti hledají řadič přes DNS záznamy)
- `-Force` → neptá se na potvrzení
- **server se sám restartuje**, pak se přihlašuješ už jako `KOTRBA\Administrator`

**Kontrola (po restartu):**
```powershell
Get-ADDomain | Select-Object Name, Forest, DomainMode
# kotrba | kotrba.cyberschool.internal | Windows2025Domain
```

---

## 4. Integrované DNS

Povýšení vytvořilo DNS zóny uložené **přímo v AD** a přepnulo DNS serveru na `127.0.0.1` (sám na sebe).

```powershell
Get-DnsServerZone | Select-Object ZoneName, ZoneType, IsDsIntegrated
Resolve-DnsName -Name "kotrba.cyberschool.internal"
```
Správně:
- `_msdcs.kotrba.cyberschool.internal` – Primary, **True**
- `kotrba.cyberschool.internal` – Primary, **True**
- doména se přeloží na `192.168.16.10`

- **IsDsIntegrated = True** → zóna je v databázi AD, replikuje se s AD a jde v ní zapnout bezpečné aktualizace
- **`_msdcs`** = zóna se servisními záznamy (SRV), přes které klienti najdou řadič domény

---

## 5. FSMO role a Global Catalog

```powershell
netdom query fsmo
Get-ADDomainController -Identity SRV1-DC | Select-Object Name, IsGlobalCatalog, OperationMasterRoles
```
Všech 5 [[FSMO]] rolí musí být na `SRV1-DC` a `IsGlobalCatalog = True`.

| Role | Úroveň | Co dělá |
| :-- | :-- | :-- |
| **Schema master** | les | jediný smí měnit schéma AD (jaké objekty a atributy existují) |
| **Domain naming master** | les | přidávání/odebírání domén v lese |
| **PDC emulator** | doména | hlavní zdroj času, změny hesel, zamykání účtů |
| **RID pool manager** | doména | rozdává bloky čísel na unikátní ID (SID) nových objektů |
| **Infrastructure master** | doména | udržuje odkazy na objekty z jiných domén |

- **Global Catalog (GC)** = částečná kopie všech objektů z celého lesa → rychlé hledání a přihlašování
- první řadič v novém lese má automaticky všechno

---

## 6. Přihlášení do domény a ADUC

Přihlášení: `KOTRBA\Administrator` nebo `Administrator@kotrba.cyberschool.internal`, heslo `Pa55w.rd`.

```powershell
whoami                                    # kotrba\administrator
Get-ADOrganizationalUnit -Filter *        # výchozí OU (Domain Controllers)
Get-ADUser -Identity Administrator | Select-Object SamAccountName, UserPrincipalName, Enabled
```
- **ADUC** (*Active Directory Users and Computers*, `dsa.msc`) = grafická správa uživatelů, skupin a OU
- **SamAccountName** = staré jméno (`Administrator`), **UserPrincipalName** = jméno ve tvaru e-mailu

---

## 7. (Nepovinné) Ověřovací skript

```powershell
powershell -ExecutionPolicy Bypass -Command "curl.exe --progress-bar -L https://raw.githubusercontent.com/DeepyCat/well_ops/main/skripty/01_check_SRV1-DC.bat -o check.bat; .\check.bat; Remove-Item -Force check.bat -ErrorAction SilentlyContinue"
```
Kontroluje i služby, které musí běžet: **NTDS** (AD), **ADWS** (webové služby AD – potřebuje je PowerShell modul), **Kdc** (Kerberos), **Netlogon**, **DNS**, a sdílené složky **SYSVOL** a **NETLOGON** (skripty a politiky domény).

---

## Rychlý postup

> [!example]- SRV1-DC
> ```powershell
> Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools
> $DomainName = "kotrba.cyberschool.internal"
> $SecurePassword = ConvertTo-SecureString "Pa55w.rd" -AsPlainText -Force
> Install-ADDSForest -DomainName $DomainName -SafeModeAdministratorPassword $SecurePassword -InstallDns:$true -Force:$true
> # restart, přihlásit KOTRBA\Administrator
> Get-ADDomain | Select-Object Name, Forest, DomainMode
> netdom query fsmo
> ```

**Další:** [[02_DHCP|Modul 02 – DHCP]]

---

**Teorie:** [[01a_Domena_a_AD]] · [[01b_Radice_domeny_a_FSMO]] · [[01c_Jmeno_domeny_a_DNS]]
