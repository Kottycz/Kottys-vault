---
aliases: [Modul 03, DNS Server, M03]
---

# Modul 03 – DNS Server

[[DNS]] server na **SRV1-DC** už běží z [[01_AD_DS|Modulu 01]]. Tady se doplní **reverzní zóna**, ruční záznamy (**A**, **PTR**, **CNAME**) a na **PC1-WIN** se otestuje překlad jmen.

> [!info] Co DNS dělá
> Překládá **jméno → IP** (dopředná zóna, např. `srv2-fs` → `192.168.16.20`) a **IP → jméno** (reverzní zóna). Počítače komunikují přes IP, lidé si pamatují jména. Typy záznamů viz [[DNS záznam]].

Předchozí: [[02_DHCP|Modul 02]]

| | SRV1-DC | PC1-WIN |
| :-- | :-- | :-- |
| IPv4 | `192.168.16.10/24` statická | `.100–.200` z DHCP |
| DNS server | `127.0.0.1` / `192.168.16.10` | `192.168.16.10` |
| Doménová přípona | `kotrba.cyberschool.internal` | `kotrba.cyberschool.internal` |

---

## SRV1-DC

### 1. Kontrola služby DNS
```powershell
Get-Service -Name DNS | Select-Object Name, Status, StartType     # Running, Automatic
Get-NetIPAddress -InterfaceAlias "Ethernet1" -AddressFamily IPv4 | Select-Object IPAddress, PrefixLength
```

### 2. Dopředná zóna (Forward Lookup Zone)

Vznikla sama při povýšení na řadič. Je **AD-integrovaná** a má **zabezpečené dynamické aktualizace**.

```powershell
$domain = (Get-ADDomain).DNSRoot
Get-DnsServerZone -Name $domain | Select-Object ZoneName, ZoneType, ReplicationScope, DynamicUpdate
Get-DnsServerResourceRecord -ZoneName $domain -RRType A -Name "srv1-dc"
```
Správně: `Primary | Domain | Secure` a A záznam `srv1-dc → 192.168.16.10`

- **ReplicationScope Domain** = zóna se kopíruje na všechny řadiče v doméně
- **DynamicUpdate Secure** = záznamy si smí sami zapsat jen počítače, které jsou **členy domény** (ověřené přes AD) → cizí stroj nepřepíše cizí záznam

### 3. Reverzní zóna

Překládá **IP → jméno** (záznamy **PTR**). Sama **nevzniká**, správce ji zakládá ručně.

```powershell
$wsX = (Get-NetIPAddress -InterfaceAlias "Ethernet1" -AddressFamily IPv4).IPAddress.Split('.')[2]
Add-DnsServerPrimaryZone -NetworkId "192.168.$wsX.0/24" -ReplicationScope "Domain" -DynamicUpdate "Secure"
```
- `$wsX` – vezme IP z `Ethernet1` (`192.168.16.10`), rozdělí ji podle teček a vezme 3. číslo → **16**. Díky tomu příkaz funguje na každém pracovišti
- zóna se jmenuje **`16.168.192.in-addr.arpa`** – IP se v reverzní zóně píše **pozpátku** (DNS čte jména zprava od nejobecnějšího, u IP je nejobecnější první číslo)

**Kontrola:**
```powershell
Get-DnsServerZone -Name "16.168.192.in-addr.arpa" | Select-Object ZoneName, ZoneType, ReplicationScope, DynamicUpdate
```

### 4. Statický A + PTR záznam pro SRV2-FS

SRV2-FS zatím neběží, takže se sám nezapíše → záznam se dělá **ručně**.

```powershell
$domain = (Get-ADDomain).DNSRoot
$wsX = (Get-NetIPAddress -InterfaceAlias "Ethernet1" -AddressFamily IPv4).IPAddress.Split('.')[2]
Add-DnsServerResourceRecordA -Name "srv2-fs" -ZoneName $domain -IPv4Address "192.168.$wsX.20" -CreatePtr
```
- `-CreatePtr` → rovnou vytvoří i **PTR** v reverzní zóně (proto se reverzní zóna zakládala dřív)

**Kontrola:**
```powershell
Get-DnsServerResourceRecord -ZoneName $domain -Name "srv2-fs" | Select-Object HostName, RecordType, @{N='IP';E={$_.RecordData.IPv4Address}}
# srv2-fs  A  192.168.16.20
```
- `@{N='IP';E={...}}` = **vypočítaný sloupec** – IP je schovaná uvnitř `RecordData`, takhle se vytáhne do tabulky

### 5. Alias CNAME `ftp`

Uživatelé se mají připojovat přes **jméno služby** (`ftp.kotrba...`), ne přes jméno serveru. Když se FTP přestěhuje, změní se jen alias.

```powershell
$domain = (Get-ADDomain).DNSRoot
Add-DnsServerResourceRecordCName -Name "ftp" -HostNameAlias "srv2-fs.$domain" -ZoneName $domain
```
**Kontrola:**
```powershell
Get-DnsServerResourceRecord -ZoneName $domain -Name "ftp" | Select-Object HostName, RecordType, @{N='HostNameAlias';E={$_.RecordData.HostNameAlias}}
# ftp  CNAME  srv2-fs.kotrba.cyberschool.internal.
```
- tečka na konci = plně kvalifikované jméno (končí kořenem DNS)

### 6. Chybějící PTR pro SRV1-DC

SRV1-DC vznikl **dřív než reverzní zóna**, takže PTR nemá → `nslookup` hlásí `Default Server: UnKnown`.

```powershell
$domain = (Get-ADDomain).DNSRoot
$wsX = (Get-NetIPAddress -InterfaceAlias "Ethernet1" -AddressFamily IPv4).IPAddress.Split('.')[2]
Add-DnsServerResourceRecordPtr -Name "10" -ZoneName "$wsX.168.192.in-addr.arpa" -PtrDomainName "srv1-dc.$domain"
```
- `-Name "10"` = poslední číslo IP (`192.168.16.`**10**), zbytek adresy je ve jméně zóny

**Kontrola:**
```powershell
Get-DnsServerResourceRecord -ZoneName "16.168.192.in-addr.arpa" -Name "10" | Select-Object HostName, RecordType, @{N='Ptr';E={$_.RecordData.PtrDomainName}}
```

---

## PC1-WIN

### 1. Kontrola DNS klienta
```powershell
Get-NetIPAddress -InterfaceAlias "Ethernet1" -AddressFamily IPv4 | Select-Object IPAddress, PrefixLength
(Get-DnsClientServerAddress -InterfaceAlias "Ethernet1" -AddressFamily IPv4).ServerAddresses   # 192.168.16.10
```

### 7. Priorita adaptérů a registrace v DNS

PC1 má dvě karty. Windows posílá provoz (i DNS dotazy) přednostně přes kartu s **nižší metrikou**. Při automatické metrice by dotazy mohly jít přes `Ethernet0` (NAT) a doménu by nenašel.

```powershell
Set-NetIPInterface -InterfaceAlias "Ethernet1" -InterfaceMetric 10   # nižší = vyšší priorita
Set-NetIPInterface -InterfaceAlias "Ethernet0" -InterfaceMetric 50

Get-NetIPInterface -InterfaceAlias "Ethernet1", "Ethernet0" -AddressFamily IPv4 | Select-Object InterfaceAlias, InterfaceMetric
Get-DnsClientServerAddress -InterfaceAlias "Ethernet1" -AddressFamily IPv4 | Select-Object InterfaceAlias, ServerAddresses

ipconfig /registerdns   # klient se hned zapíše do DNS (A záznam pc1-win)
ipconfig /flushdns      # smaže lokální cache DNS – další dotazy půjdou čerstvě na server
```
- metrika se jen **mění**, na `Ethernet0` se nic nevypíná ani nepřenastavuje IP

### 8. Dopředný překlad (jméno → IP)
```powershell
nslookup srv2-fs
Resolve-DnsName -Name "srv2-fs" | Select-Object Name, Type, IPAddress
# srv2-fs.kotrba.cyberschool.internal  A  192.168.16.20
```
- stačí krátké jméno `srv2-fs` – Windows si doplní **příponu domény**, kterou dostal z DHCP (volba 015)
- nesmí se objevit `Non-existent domain`

### 9. Reverzní překlad (IP → jméno)
```powershell
nslookup 192.168.16.20
nslookup 192.168.16.10
Resolve-DnsName "192.168.16.20" | Select-Object Name, Type, NameHost
# 20.16.168.192.in-addr.arpa  Ptr  srv2-fs.kotrba.cyberschool.internal
```
- teď už `nslookup` píše `Default Server: srv1-dc.kotrba...` místo `UnKnown` (díky PTR z úkolu 6)

### 10. Alias CNAME
```powershell
Resolve-DnsName -Name "ftp.kotrba.cyberschool.internal" -Server 192.168.16.10 | Select-Object Name, Type, NameHost, IPAddress
nslookup ftp.kotrba.cyberschool.internal 192.168.16.10
```
Vrátí dva řádky: `ftp → CNAME → srv2-fs` a `srv2-fs → A → 192.168.16.20` – DNS server alias rovnou dořeší až na IP.
- `-Server 192.168.16.10` = ptá se přímo SRV1-DC, ne podle nastavení karty

### 11. Ping přes jméno
```powershell
ping srv2-fs
Test-NetConnection -ComputerName "srv2-fs" -WarningAction SilentlyContinue | Select-Object ComputerName, RemoteAddress
# srv2-fs  192.168.16.20
```
- když SRV2-FS zrovna neběží, ping neodpoví – úkol ověřuje hlavně **překlad jména** (`RemoteAddress = 192.168.16.20`)

---

## Ověřovací skripty (nepovinné)
```powershell
powershell -ExecutionPolicy Bypass -Command "curl.exe --progress-bar -L https://raw.githubusercontent.com/DeepyCat/well_ops/main/skripty/03_check_SRV1-DC.bat -o check.bat; .\check.bat; Remove-Item -Force check.bat -ErrorAction SilentlyContinue"
```
Na PC1 konec `03_check_PC1-WIN.bat`.

---

## Rychlý postup

> [!example]- SRV1-DC
> ```powershell
> $domain = (Get-ADDomain).DNSRoot
> $wsX = (Get-NetIPAddress -InterfaceAlias "Ethernet1" -AddressFamily IPv4).IPAddress.Split('.')[2]
> Add-DnsServerPrimaryZone -NetworkId "192.168.$wsX.0/24" -ReplicationScope "Domain" -DynamicUpdate "Secure"
> Add-DnsServerResourceRecordA -Name "srv2-fs" -ZoneName $domain -IPv4Address "192.168.$wsX.20" -CreatePtr
> Add-DnsServerResourceRecordCName -Name "ftp" -HostNameAlias "srv2-fs.$domain" -ZoneName $domain
> Add-DnsServerResourceRecordPtr -Name "10" -ZoneName "$wsX.168.192.in-addr.arpa" -PtrDomainName "srv1-dc.$domain"
> ```

> [!example]- PC1-WIN
> ```powershell
> Set-NetIPInterface -InterfaceAlias "Ethernet1" -InterfaceMetric 10
> Set-NetIPInterface -InterfaceAlias "Ethernet0" -InterfaceMetric 50
> ipconfig /registerdns; ipconfig /flushdns
> nslookup srv2-fs
> nslookup 192.168.16.20
> nslookup ftp.kotrba.cyberschool.internal 192.168.16.10
> ```
