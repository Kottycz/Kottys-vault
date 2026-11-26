---
aliases: [Modul 00, Příprava a instalace OS, M00]
---

# Modul 00 – Příprava a instalace OS

Příprava všech tří strojů: **SRV1-DC** (budoucí řadič domény), **SRV2-FS** (souborový server) a **PC1-WIN** (klient). Pravidla sítě a hesla jsou v [[Rules]].

> [!info] Moje hodnoty (pracoviště 16)
> - síť `192.168.16.0/24`, brána `.1`
> - **SRV1-DC** = `.10`, **SRV2-FS** = `.20`, **PC1-WIN** = DHCP (`.100–.200`)
> - heslo všude `Pa55w.rd`

Všechny příkazy se pouští v **PowerShellu jako Administrator** (64bit, ne „(x86)“).

---

## 1. Parametry virtuálního stroje

Nastavuje se v **CyLabu** (hypervizoru), ne ve Windows.

| Parametr | SRV1-DC | SRV2-FS | PC1-WIN |
| :-- | :-- | :-- | :-- |
| vCPU | 2 | 2 | 2 |
| RAM | 8 GB | 8 GB | 8 GB |
| Systémový disk | 100 GB | 100 GB | **60 GB** |
| Další disky | – | **5× disk** (zadání 10, víc CyLab nedovolí) | – |
| Sítě | NIC 1, **NIC 2 (zapnout!)**, NIC 3 | stejně | stejně |

**Kontrola:**
```powershell
Get-Disk | Select-Object Number, FriendlyName, Size
# SRV2-FS i se stylem oddílů – datové disky mají být RAW:
Get-Disk | Select-Object Number, FriendlyName, Size, PartitionStyle
```
- `Get-Disk` vypíše všechny disky, které Windows vidí → hned poznáš, jestli VM dostala správnou velikost
- **RAW** = disk ještě nebyl inicializovaný (žádná tabulka oddílů) → na SRV2-FS se z nich později udělá Storage Pool

---

## 2. Edice a instalace Windows

| Stroj | Edice | Rozhraní | Jazyk média |
| :-- | :-- | :-- | :-- |
| SRV1-DC, SRV2-FS | **Windows Server 2025 Datacenter** | **Desktop Experience** (s GUI), ne Server Core | English (US) |
| PC1-WIN | **Windows 11 Education N** (EU edice bez multimédií) | – | English (US) |

**Kontrola:**
```powershell
Get-ComputerInfo | Select-Object WindowsProductName, OsServerLevel
```
- `OsServerLevel : FullServer` = je tam GUI (Desktop Experience); `ServerCore` by bylo špatně

### PC1-WIN – instalace bez Microsoft účtu (OOBE)

Windows 11 v průvodci prvního spuštění ([[OOBE]]) vynucuje Microsoft účet, když má internet. Proto se internet „odebere“:

1. V CyLabu **odpojit NIC 1** (odškrtnout *Connected*) → stroj nemá internet
2. Nainstalovat Windows 11 Education N (English US)
3. V OOBE stisknout **Shift + F10** (příp. Fn + Shift + F10) → otevře se příkazový řádek:
   ```
   oobe\bypassnro
   ```
   PC se restartuje. Příkaz zapne skrytou volbu „bez sítě“.
4. Na obrazovce sítě: **I don't have internet** → **Continue with limited setup**
5. Uživatel **`temp`** (jméno *Administrator* OOBE nepovolí – je rezervované)
6. Po přepnutí na Administratora (úkol 5) **NIC 1 zase připojit**

---

## 3. Jméno počítače (Hostname)

```powershell
Rename-Computer -NewName "SRV1-DC" -Restart   # na SRV2-FS: "SRV2-FS", na PC1: "PC1-WIN"
```
- `-Restart` → nové jméno platí až po restartu, tak se rovnou restartuje
- jméno musí být hotové **před** povýšením na řadič domény (pak se mění špatně)

**Kontrola:** `hostname`

---

## 4. Nastavení TCP/IPv4

> [!warning] Pravidla síťovek
> - **NIC 1 = `Ethernet0`** → NAT, internet, správa. **NEŠAHAT.**
> - **NIC 2 = `Ethernet1`** → interní lab síť, **tady se nastavuje IP**. Musí být zapnutá v CyLabu.
> - **NIC 3 = `Ethernet2`** → třídní síť, nechat podle učitele.
>
> V CyLabu se adaptéry jmenují `Ethernet1` **bez mezery**. Když je to u tebe `Ethernet 1`, uprav `-InterfaceAlias`.

### Servery (statická IP)

| | IP | Brána | DNS |
| :-- | :-- | :-- | :-- |
| SRV1-DC | `192.168.16.10/24` | `192.168.16.1` | `192.168.16.10` (sám na sebe – bude DNS server) |
| SRV2-FS | `192.168.16.20/24` | `192.168.16.1` | `192.168.16.10` (ukazuje na SRV1-DC) |

```powershell
# 1. Seznam adaptérů – najdi Ethernet1
Get-NetAdapter

# 2. Statická IP + brána (na SRV2-FS IP .20)
New-NetIPAddress -InterfaceAlias "Ethernet1" -IPAddress "192.168.16.10" -PrefixLength 24 -DefaultGateway "192.168.16.1"

# 3. DNS server
Set-DnsClientServerAddress -InterfaceAlias "Ethernet1" -ServerAddresses ("192.168.16.10")
```
- `-PrefixLength 24` = maska `255.255.255.0`
- servery mají **pevnou** adresu, aby je klienti vždycky našli (DNS, DHCP, doména)

### Povolení pingu (firewall)

Windows ve výchozím stavu **blokuje příchozí ping** (ICMP Echo Request) → `ping` hlásí *Request timed out*, i když síť funguje.

```powershell
New-NetFirewallRule -Name "Allow-Ping-In-IPv4"  -DisplayName "Allow ICMPv4-In (Ping)"  -Protocol ICMPv4 -IcmpType 8   -Direction Inbound  -Action Allow -Profile Any
New-NetFirewallRule -Name "Allow-Ping-In-IPv6"  -DisplayName "Allow ICMPv6-In (Ping)"  -Protocol ICMPv6 -IcmpType 128 -Direction Inbound  -Action Allow -Profile Any
New-NetFirewallRule -Name "Allow-Ping-Out-IPv4" -DisplayName "Allow ICMPv4-Out (Ping)" -Protocol ICMPv4 -IcmpType 8   -Direction Outbound -Action Allow -Profile Any
New-NetFirewallRule -Name "Allow-Ping-Out-IPv6" -DisplayName "Allow ICMPv6-Out (Ping)" -Protocol ICMPv6 -IcmpType 128 -Direction Outbound -Action Allow -Profile Any
```
- **IcmpType 8** = Echo Request v IPv4, **128** = Echo Request v IPv6
- `-Profile Any` → platí v síti Domain, Private i Public

### PC1-WIN (DHCP)

Klient **nemá statickou IP** – dostane ji v [[02_DHCP|Modulu 02]] z DHCP serveru.

```powershell
Get-NetAdapter

# Ping jedním příkazem – zapne vestavěné pravidlo
Enable-NetFirewallRule -Name "FPS-ICMP4-ERQ-In"

# Ethernet1 na DHCP + DNS automaticky
Set-NetIPInterface -InterfaceAlias "Ethernet1" -Dhcp Enabled
Set-DnsClientServerAddress -InterfaceAlias "Ethernet1" -ResetServerAddresses
```
- `FPS-ICMP4-ERQ-In` = existující pravidlo *File and Printer Sharing (Echo Request – ICMPv4-In)*, jen se zapne
- `-ResetServerAddresses` = smaže ručně zadané DNS → bere je z DHCP

> [!note] Proč z PC1 zatím nejde ping
> Dokud neběží DHCP server, PC1 nedostane adresu (má jen APIPA `169.254.x.x`). Na dočasný test jde nastavit `192.168.16.100/24` ručně, ale **k odevzdání vrátit na DHCP**.

### Kontrola
```powershell
Get-NetIPAddress -AddressFamily IPv4 -InterfaceAlias Ethernet1 | Select-Object IPAddress, PrefixLength, PrefixOrigin
Get-NetIPConfiguration -InterfaceAlias Ethernet1 | Select-Object -ExpandProperty IPv4DefaultGateway
Get-DnsClientServerAddress -InterfaceAlias Ethernet1 -AddressFamily IPv4 | Select-Object InterfaceAlias, ServerAddresses
Test-NetConnection -ComputerName "192.168.16.20" -InformationLevel Detailed   # ze SRV1 na SRV2 (a naopak .10)

# PC1:
Get-NetIPInterface -InterfaceAlias Ethernet1 -AddressFamily IPv4 | Select-Object InterfaceAlias, Dhcp
Get-NetFirewallRule -Name "FPS-ICMP4-ERQ-In" | Select-Object DisplayName, Direction, Action, Enabled
```
- **PrefixOrigin**: `Manual` = statická (servery), `Dhcp` = z DHCP (PC1); dokud DHCP server neběží, má PC1 jen automatickou adresu `169.254.x.x` (APIPA)
- `Test-NetConnection` → hledej `PingSucceeded : True`

---

## 5. Účet administrátora a heslo

**Servery:** heslo vestavěného účtu `Administrator` = `Pa55w.rd` se nastaví už při instalaci. Žádný jiný admin účet se nevytváří.

**PC1-WIN:** Administrator je ve Windows 11 vypnutý → zapnout ho z účtu `temp`:
```powershell
Enable-LocalUser -Name "Administrator"
Set-LocalUser -Name "Administrator" -Password ("Pa55w.rd" | ConvertTo-SecureString -AsPlainText -Force)
```
- `ConvertTo-SecureString` – parametr `-Password` nebere obyčejný text, ale zabezpečený řetězec
- pak **odhlásit temp → přihlásit Administrator** → smazat temp (účet, pod kterým jsi přihlášený, smazat nejde):
```powershell
Remove-LocalUser -Name "temp"
```

**Kontrola:** `Get-LocalUser | Select-Object Name, Enabled` → `Administrator True`, žádný `temp`

---

## 6. Jazyk, region a formáty (cs-CZ)

Formáty a poloha česky, **rozhraní zůstává anglicky** (kvůli odborným pojmům a návodům).

```powershell
Set-Culture cs-CZ               # formáty data, čísel, měny pro uživatele
Set-WinSystemLocale cs-CZ       # jazyk pro programy bez Unicode – projeví se až po RESTARTU
Set-WinHomeLocation -GeoId 0x4b # poloha Česko (0x4b = 75)
```

**Kontrola:**
```powershell
Get-Culture | Select-Object Name, DisplayName   # cs-CZ, Czech (Czechia)
Get-WinSystemLocale                              # cs-CZ (po restartu!)
Get-WinHomeLocation                              # 75
Get-WinUILanguageOverride                        # prázdné nebo en-US
```

---

## 7. Formáty data, času a měny

Většinou hotové už díky `Set-Culture`. Ručně: *Settings → Time & language → Language & region → Regional format: Czech (Czechia)*.

**Kontrola:**
```powershell
Get-Date -Format "d.M.yyyy H:mm:ss"   # např. 20.9.2026 13:45:02
(12345.67).ToString("C")              # 12 345,67 Kč
```
- `"C"` = formát měny podle aktuální kultury → když vyjde `Kč`, kultura je správně

---

## 8. Časové pásmo (Praha)

```powershell
Set-TimeZone -Id "Central Europe Standard Time"
```
- **proč:** Active Directory ověřuje přes **Kerberos** a ten odmítne přihlášení, když se čas strojů liší o víc než 5 minut

**Kontrola:** `Get-TimeZone` → `(UTC+01:00) ... Prague`

---

## 9. Klávesnice US a Czech (QWERTZ)

US jako první (příkazy se líp píšou – `\`, `|`, `$` jsou na místě), čeština jako druhá. Přepínání **Win + mezerník**.

```powershell
$List = New-WinUserLanguageList "en-US"
$List.Add("cs-CZ")
Set-WinUserLanguageList $List -Force
```
- vytvoří se nový seznam jazyků, přidá se čeština a seznam se nastaví celý najednou (`-Force` = bez ptaní)

**Kontrola:**
```powershell
Get-WinUserLanguageList | Select-Object LanguageTag, InputMethodTips
# en-US {0409:00000409}, cs-CZ {0405:00000405}
Get-ItemProperty "HKCU:\Keyboard Layout\Preload"   # 1 = 00000409 (US), 2 = 00000405 (CZ)
```

---

## 10. Telemetrie a diagnostika na minimum

Zápis **politik do registru** – stejné, jako kdyby to nastavila skupinová politika (GPO).

```powershell
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\DataCollection"   /v AllowTelemetry        /t REG_DWORD /d 1 /f
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\LocationAndSensors" /v DisableLocation      /t REG_DWORD /d 1 /f
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\AdvertisingInfo"  /v DisabledByGroupPolicy /t REG_DWORD /d 1 /f
```
| Hodnota | Význam |
| :-- | :-- |
| `AllowTelemetry = 1` | jen povinná diagnostická data (Required) |
| `DisableLocation = 1` | poloha vypnutá |
| `DisabledByGroupPolicy = 1` | reklamní ID vypnuté |

- `/v` název hodnoty, `/t` typ, `/d` data, `/f` přepsat bez ptaní

**Kontrola:**
```powershell
Get-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection" -Name AllowTelemetry
Get-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\LocationAndSensors" -Name DisableLocation
Get-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\AdvertisingInfo" -Name DisabledByGroupPolicy
```

---

## 11. Aktivace Windows (LAB KEY)

Klíč je v zadání v Teams – **do dokumentace ho nepsat**.

```powershell
slmgr.vbs /ipk <LAB-KEY-Z-TEAMS>   # install product key
slmgr.vbs /ato                     # activate online
```
**Kontrola:** `slmgr.vbs /xpr` → *The machine is permanently activated* (nebo datum u KMS). `slmgr.vbs /dli` ukáže info o licenci.

---

## 12. PC1-WIN – pouze lokální účet (úklid)

Rekapitulace: odpojit NIC 1 → `oobe\bypassnro` → *limited setup* → účet `temp` → zapnout Administratora → přepnout se → smazat temp → připojit NIC 1.

```powershell
Get-LocalUser | Select-Object Name, Enabled
Remove-LocalUser -Name "temp" -ErrorAction SilentlyContinue
```
Správně: `Administrator True`, `DefaultAccount / Guest / WDAGUtilityAccount False` – nic dalšího.

---

## 13. (Nepovinné) Ověřovací skript

Jen čte konfiguraci, nic nemění a po sobě se smaže. Na konci zeptá na číslo pracoviště (16).

```powershell
powershell -ExecutionPolicy Bypass -Command "curl.exe --progress-bar -L https://raw.githubusercontent.com/DeepyCat/well_ops/main/skripty/00_check_SRV1-DC.bat -o check.bat; .\check.bat; Remove-Item -Force check.bat -ErrorAction SilentlyContinue"
```
- pro ostatní stroje změň konec na `00_check_SRV2-FS.bat` / `00_check_PC1-WIN.bat`
- výsledek: `[ OK ]` splněno, `[KONTROLA]` zkontrolovat ručně (heslo, licence), `[CHYBA]` opravit

---

## Rychlý postup po strojích

> [!example]- SRV1-DC
> ```powershell
> Rename-Computer -NewName "SRV1-DC" -Restart
> New-NetIPAddress -InterfaceAlias "Ethernet1" -IPAddress "192.168.16.10" -PrefixLength 24 -DefaultGateway "192.168.16.1"
> Set-DnsClientServerAddress -InterfaceAlias "Ethernet1" -ServerAddresses ("192.168.16.10")
> # + 4× New-NetFirewallRule (ping)
> Set-Culture cs-CZ; Set-WinSystemLocale cs-CZ; Set-WinHomeLocation -GeoId 0x4b
> Set-TimeZone -Id "Central Europe Standard Time"
> $List = New-WinUserLanguageList "en-US"; $List.Add("cs-CZ"); Set-WinUserLanguageList $List -Force
> # + 3× reg add (telemetrie)
> slmgr.vbs /ipk <KLIC>; slmgr.vbs /ato
> Restart-Computer
> ```

> [!example]- SRV2-FS
> Stejné jako SRV1-DC, jen jméno `SRV2-FS` a IP **`192.168.16.20`** (DNS zůstává `.10`). V CyLabu navíc 5 datových disků.

> [!example]- PC1-WIN
> ```powershell
> # instalace: odpojit NIC1 → Shift+F10 → oobe\bypassnro → limited setup → účet temp
> Enable-LocalUser -Name "Administrator"
> Set-LocalUser -Name "Administrator" -Password ("Pa55w.rd" | ConvertTo-SecureString -AsPlainText -Force)
> # odhlásit, přihlásit jako Administrator
> Remove-LocalUser -Name "temp"
> # připojit NIC1 v CyLabu
> Rename-Computer -NewName "PC1-WIN" -Restart
> Enable-NetFirewallRule -Name "FPS-ICMP4-ERQ-In"
> Set-NetIPInterface -InterfaceAlias "Ethernet1" -Dhcp Enabled
> Set-DnsClientServerAddress -InterfaceAlias "Ethernet1" -ResetServerAddresses
> # lokalizace, čas, klávesnice, telemetrie, aktivace – stejně jako servery
> ```

**Další:** [[01_AD_DS|Modul 01 – AD DS]]

---

**Teorie:** [[00a_Virtualizace_edice_aktivace]] · [[00b_Identita_a_sit]] · [[00c_Cas_jazyk_soukromi]]
