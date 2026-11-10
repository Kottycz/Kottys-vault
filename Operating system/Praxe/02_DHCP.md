---
aliases: [Modul 02, DHCP Server, M02]
---

# Modul 02 – DHCP Server

Na **SRV1-DC** se nastaví [[DHCP]] server, aby **PC1-WIN** dostal IP adresu, bránu a DNS automaticky.

> [!info] Jak DHCP funguje (DORA)
> Klient nemá adresu → pošle do sítě **Discover** (broadcast) → server nabídne adresu (**Offer**) → klient o ni požádá (**Request**) → server potvrdí (**Ack**). Adresa je **zapůjčená (lease)** na určitou dobu, pak se obnovuje.

Předchozí: [[01_AD_DS|Modul 01]]

> [!warning] Jen `Ethernet1`
> Všechno se dělá na **NIC 2 = `Ethernet1`**. Na `Ethernet0` (NAT) nesahat.

---

## SRV1-DC

### 1. Kontrola předpokladů

| | SRV1-DC (server) | PC1-WIN (klient) |
| :-- | :-- | :-- |
| Stav | řadič domény z Modulu 01 | Windows 11 z Modulu 00 |
| IPv4 | `192.168.16.10/24` statická | z DHCP |
| Brána | `192.168.16.1` | `192.168.16.1` (přidělí DHCP) |
| Doména | `kotrba.cyberschool.internal` | zatím WORKGROUP |

```powershell
hostname
Get-NetIPAddress -InterfaceAlias Ethernet1 -AddressFamily IPv4 | Select-Object IPAddress, PrefixLength
Get-ADDomain | Select-Object Name, Forest
```

### 2. Instalace role DHCP

```powershell
Install-WindowsFeature -Name DHCP -IncludeManagementTools
```
**Kontrola:** `Get-WindowsFeature -Name DHCP, RSAT-DHCP | Select-Object Name, InstallState` → obojí *Installed*

### 3. Bezpečnostní skupiny a restart služby

Po instalaci je potřeba **dokončit konfiguraci** (post-install):

```powershell
Add-DhcpServerSecurityGroup            # vytvoří skupiny DHCP Administrators a DHCP Users
Restart-Service -Name DHCPServer       # služba si načte nová oprávnění

# volitelně – schová žlutou vlaječku "Complete DHCP configuration" v Server Manageru
Set-ItemProperty -Path 'registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ServerManager\Roles\12' -Name 'ConfigurationState' -Value 2
```
- **DHCP Administrators** = smí DHCP spravovat, **DHCP Users** = smí jen číst
- na řadiči domény nejsou lokální skupiny → skupiny vzniknou **v AD**, proto se kontrolují přes `Get-ADGroup`, ne `Get-LocalGroup`
- místo příkazů jde i průvodce v Server Manageru: vlaječka → *Complete DHCP configuration* → Next → Commit → Close (udělá úkoly 3 i 4)

**Kontrola:**
```powershell
Get-Service -Name DHCPServer | Select-Object Name, Status, StartType   # Running, Automatic
Get-ADGroup -Filter 'Name -like "DHCP*"' | Select-Object Name           # DHCP Administrators, DHCP Users
```

### 4. Autorizace DHCP serveru v AD

V doméně smí adresy rozdávat **jen autorizovaný** DHCP server. Neautorizovaný se sám zablokuje → ochrana proti podvrženým (**rogue**) DHCP serverům.

```powershell
$DnsName = "$env:COMPUTERNAME.$((Get-ADDomain).DNSRoot)"
$DnsName                               # SRV1-DC.kotrba.cyberschool.internal
Add-DhcpServerInDC -DnsName $DnsName -IPAddress "192.168.16.10"
```
- `$env:COMPUTERNAME` = jméno stroje, `(Get-ADDomain).DNSRoot` = jméno domény → spojené dají **FQDN** (plné jméno)

**Kontrola:** `Get-DhcpServerInDC | Select-Object DnsName, IPAddress`

### 5. Scope (rozsah adres)

| Parametr | Hodnota |
| :-- | :-- |
| Název | `Ucebna` |
| ScopeId (síť) | `192.168.16.0` |
| Rozsah | `192.168.16.100` – `192.168.16.200` |
| Maska | `255.255.255.0` (/24) |
| Stav | `Active` |

```powershell
Add-DhcpServerv4Scope -Name "Ucebna" -StartRange "192.168.16.100" -EndRange "192.168.16.200" -SubnetMask "255.255.255.0" -State Active
```
- adresy **.1–.99** zůstávají pro zařízení s pevnou IP (brána .1, servery .10, .20, .30) → DHCP je nikdy nerozdá, takže nehrozí konflikt
- **ScopeId** se dopočítá z rozsahu a masky
- víc o pojmu: [[DHCP scope]]

**Kontrola:** `Get-DhcpServerv4Scope | Select-Object ScopeId, Name, StartRange, EndRange, State`

### 6. DHCP volby (options)

Kromě IP a masky musí klient dostat i bránu, DNS a doménu.

| Volba | Kód | Hodnota |
| :-- | :-- | :-- |
| Router (brána) | **003** | `192.168.16.1` |
| DNS server | **006** | `192.168.16.10` |
| DNS doména | **015** | `kotrba.cyberschool.internal` |

```powershell
$DomainName = (Get-ADDomain).DNSRoot
Set-DhcpServerv4OptionValue -ScopeId "192.168.16.0" -Router "192.168.16.1" -DnsServer "192.168.16.10" -DnsDomain $DomainName
```
- DNS musí být **SRV1-DC** – jinak by klient nenašel doménu (a nešel by do ní později přidat)
- `-DnsServer` cmdlet ověřuje, že na adrese opravdu běží DNS server

**Kontrola:**
```powershell
Get-DhcpServerv4OptionValue -ScopeId "192.168.16.0" | Select-Object OptionId, Name, Value
```
Navíc tam je **Option 51 Lease = 691200** → výchozí doba zápůjčky **8 dní** (691200 s).

### 8. Kontrola zápůjček (po úkolu 7 na PC1)

```powershell
Get-DhcpServerv4Lease -ScopeId "192.168.16.0" | Select-Object IPAddress, HostName, ClientId, AddressState, LeaseExpiryTime
```
Správně: `192.168.16.100 | PC1-WIN | Active`
- **ClientId** = MAC adresa klienta – podle ní server pozná, komu adresu půjčil
- graficky: `dhcpmgmt.msc` → server má **zelenou** ikonu = aktivní a autorizovaný

---

## PC1-WIN

### 1. Kontrola adaptéru
```powershell
Get-NetAdapter -Name Ethernet1 | Select-Object Name, Status, LinkSpeed   # Up
```

### 7. Zapnutí DHCP klienta
```powershell
Set-NetIPInterface -InterfaceAlias "Ethernet1" -Dhcp Enabled
Set-DnsClientServerAddress -InterfaceAlias "Ethernet1" -ResetServerAddresses

ipconfig /release Ethernet1   # vrátí starou adresu
ipconfig /renew Ethernet1     # požádá DHCP o novou (proběhne DORA)
```
> [!warning] Vždy psát `Ethernet1`
> Samotné `ipconfig /release` bez jména uvolní **všechny** adaptéry včetně `Ethernet0` → přijdeš o internet i o přístup.

**Kontrola:**
```powershell
Get-NetIPAddress -InterfaceAlias Ethernet1 -AddressFamily IPv4 | Select-Object IPAddress, PrefixLength, PrefixOrigin
Get-NetIPConfiguration -InterfaceAlias Ethernet1 | Select-Object -ExpandProperty IPv4DefaultGateway
Get-DnsClientServerAddress -InterfaceAlias Ethernet1 -AddressFamily IPv4 | Select-Object ServerAddresses
```
Správně: `192.168.16.100 /24 Dhcp`, brána `.1`, DNS `.10`

### 9. Test obnovení a konektivity
```powershell
ipconfig /release Ethernet1
ipconfig /renew Ethernet1
Test-NetConnection -ComputerName "192.168.16.10" -InformationLevel Detailed   # PingSucceeded : True
Resolve-DnsName -Name "srv1-dc.kotrba.cyberschool.internal"                   # 192.168.16.10
```
- `Resolve-DnsName` funguje jen proto, že DHCP předal DNS server `.10` → důkaz, že volby 006 dorazily

> [!note] Dva záznamy srv1-dc
> `Resolve-DnsName` může vrátit i adresu z `Ethernet0` (10.x.x.x), protože se server zaregistroval do DNS z obou karet. Řeší se v [[03_DNS|Modulu 03]].

---

## Ověřovací skripty (nepovinné)
```powershell
powershell -ExecutionPolicy Bypass -Command "curl.exe --progress-bar -L https://raw.githubusercontent.com/DeepyCat/well_ops/main/skripty/02_check_SRV1-DC.bat -o check.bat; .\check.bat; Remove-Item -Force check.bat -ErrorAction SilentlyContinue"
```
Na PC1 konec `02_check_PC1-WIN.bat`.

---

## Rychlý postup

> [!example]- SRV1-DC
> ```powershell
> Install-WindowsFeature -Name DHCP -IncludeManagementTools
> Add-DhcpServerSecurityGroup
> Restart-Service -Name DHCPServer
> $DnsName = "$env:COMPUTERNAME.$((Get-ADDomain).DNSRoot)"
> Add-DhcpServerInDC -DnsName $DnsName -IPAddress "192.168.16.10"
> Add-DhcpServerv4Scope -Name "Ucebna" -StartRange "192.168.16.100" -EndRange "192.168.16.200" -SubnetMask "255.255.255.0" -State Active
> $DomainName = (Get-ADDomain).DNSRoot
> Set-DhcpServerv4OptionValue -ScopeId "192.168.16.0" -Router "192.168.16.1" -DnsServer "192.168.16.10" -DnsDomain $DomainName
> # po PC1:
> Get-DhcpServerv4Lease -ScopeId "192.168.16.0"
> ```

> [!example]- PC1-WIN
> ```powershell
> Set-NetIPInterface -InterfaceAlias "Ethernet1" -Dhcp Enabled
> Set-DnsClientServerAddress -InterfaceAlias "Ethernet1" -ResetServerAddresses
> ipconfig /release Ethernet1
> ipconfig /renew Ethernet1
> Test-NetConnection -ComputerName "192.168.16.10"
> ```

**Další:** [[03_DNS|Modul 03 – DNS]]
