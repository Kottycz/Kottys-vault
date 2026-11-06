# Modul 0 — Příprava — postup

> Šablona verze: 2026-10-03 · Vyplňte všechna místa `DOPLNIT`. **Nadpisy ani ID neměňte** — podle nich se vaše práce porovnává se vzorovým řešením. Pravidla viz [[00-pravidla-prace-s-vaultem]].

Ke každé části popište, **co jste skutečně udělali**: kroky v GUI (kde jste klikli, jaké hodnoty jste zadali) nebo příkazy, které jste spustili — v pořadí, jak jste je prováděli. Příkazy vkládejte i s promptem.

## Údaje o řešiteli

| Položka | Hodnota |
|---|---|
| Jméno a příjmení | Matěj Kotrba |
| Třída | T3A |
| Datum vypracování | 25. 10. 2026 |
| Vaše doména | kotrba.cyberschool.internal |

## SRV1-DC

### M0-SRV1.P1 Vytvoření VM a instalace OS

**M0-SRV1.P1** – Postup — parametry VM, které jste nastavili (vCPU, RAM, disky), zvolená edice a jazyk instalace

```text
VM v CyLabu: 2 vCPU, 8192 MB RAM, disk 100 GB.
Edice: Windows Server 2025 Datacenter (Desktop Experience), jazyk instalace English (United States).
Instalace: Custom: Install Windows only, instalováno na 100GB disk.
```

![[m0-srv1-v1-1.png]]

- [x] Hotovo

### M0-SRV1.P2 Účet administrátora

**M0-SRV1.P2** – Postup — jak jste nastavili heslo vestavěného účtu Administrator

```text
Při instalaci Windows Serveru jsem na obrazovce Customize settings zadal heslo vestavěného účtu Administrator: Pa55w.rd (zadáno dvakrát, Finish). Na účet se pak přihlašuji jako Administrator s tímto heslem.
```

<!-- nebo místo výpisu vložte screenshot (Ctrl+V) s viditelnými hodinami -->

- [x] Hotovo

### M0-SRV1.P3 Jméno počítače a síť

**M0-SRV1.P3** – Postup — přejmenování počítače a statické nastavení TCP/IPv4 (hodnoty, které jste zadali)

```text
Příkazy v PowerShellu (Run as Administrator):
Rename-Computer -NewName SRV1-DC -Force
New-NetIPAddress -InterfaceAlias Ethernet1 -IPAddress 192.168.16.10 -PrefixLength 24 -DefaultGateway 192.168.16.1
Set-DnsClientServerAddress -InterfaceAlias Ethernet1 -ServerAddresses 192.168.16.10
Restart-Computer
(Ethernet1 = síťová karta NIC 2 do sandboxu; podsíť 192.168.16.0/24, brána .1, DNS = sám server .10)
```

![[m0-srv1-v4-1.png]]

![[m0-srv1-v4-2.png]]

- [x] Hotovo

### M0-SRV1.P4 Aktivace

**M0-SRV1.P4** – Postup — jakým způsobem jste Windows aktivovali (při instalaci / v Settings / příkazem)

```text
Aktivace příkazem (produktový klíč pro CyLab z Teams):
slmgr.vbs /ipk <produktový klíč pro server>
slmgr.vbs /ato
Kontrola: slmgr.vbs /xpr a slmgr.vbs /dli
```

![[m0-srv1-v11-1.png]]

- [x] Hotovo

### M0-SRV1.P5 Jazyk, region, klávesnice, časové pásmo, home location

**M0-SRV1.P5** – Postup — co jste kde nastavili a na jaké hodnoty

```text
Set-TimeZone -Id "Central Europe Standard Time"
Set-Culture cs-CZ
Set-WinSystemLocale cs-CZ
Set-WinHomeLocation -GeoId 75
Set-WinUserLanguageList -LanguageList en-US,cs-CZ -Force
Výsledek: display language English (US), region Czech (cs-CZ), časové pásmo (UTC+01:00) Central Europe, home location Czechia (GeoId 75), klávesnice en-US + Czech (QWERTZ), přepínání Win+Space.
```

![[m0-srv1-v6-1.png]]

![[m0-srv1-v9-1.png]]

- [x] Hotovo

### M0-SRV1.P6 Soukromí a telemetrie

**M0-SRV1.P6** – Postup — která nastavení soukromí jste změnili

```text
Nastavení přes registry (politiky):
HKLM\SOFTWARE\Policies\Microsoft\Windows\DataCollection  AllowTelemetry = 1 (Required diagnostic data)
HKLM\SOFTWARE\Policies\Microsoft\Windows\LocationAndSensors  DisableLocation = 1
HKLM\SOFTWARE\Policies\Microsoft\Windows\AdvertisingInfo  DisabledByGroupPolicy = 1
```

![[m0-srv1-v10-1.png]]

![[m0-srv1-v10-2.png]]

- [x] Hotovo

### M0-SRV1.P7 PowerShell prompt s otiskem

**M0-SRV1.P7** – Postup — spuštění bloku pro nastavení promptu (vložte i jeho výstup / nové okno s promptem)

```text
Set-ExecutionPolicy -Scope LocalMachine -ExecutionPolicy RemoteSigned -Force
$p = $PROFILE.AllUsersAllHosts
if (-not (Test-Path $p)) { New-Item -Path $p -ItemType File -Force | Out-Null }
if (-not (Select-String -Path $p -Pattern 'OPS_PROMPT' -Quiet)) {
Add-Content -Path $p -Value @'
# OPS_PROMPT
function prompt { "[$(Get-Date -Format 'yyyy-MM-dd HH:mm:ss')] $env:USERDOMAIN\$env:USERNAME@$env:COMPUTERNAME PS $($executionContext.SessionState.Path.CurrentLocation)> " }
'@
}
. $p
Prompt má tvar: [datum čas] SRV1-DC\Administrator@SRV1-DC PS C:\...>  (výstup z nového okna vložit screenshotem)
```

![[m0-srv1-v13-1.png]]

![[m0-srv1-v13-2.png]]

![[m0-srv1-v13-3.png]]

- [x] Hotovo

## SRV2-FS

> SRV2-FS připravujete až před Modulem 6 — tuto část vyplňte a odevzdejte znovu s Modulem 6.

### M0-SRV2.P1 Vytvoření VM a instalace OS

**M0-SRV2.P1** – Postup — parametry VM, které jste nastavili (vCPU, RAM, disky), zvolená edice a jazyk instalace

```text
DOPLNIT
```

<!-- nebo místo výpisu vložte screenshot (Ctrl+V) s viditelnými hodinami -->

- [ ] Hotovo

### M0-SRV2.P2 Účet administrátora

**M0-SRV2.P2** – Postup — jak jste nastavili heslo vestavěného účtu Administrator

```text
DOPLNIT
```

<!-- nebo místo výpisu vložte screenshot (Ctrl+V) s viditelnými hodinami -->

- [ ] Hotovo

### M0-SRV2.P3 Jméno počítače a síť

**M0-SRV2.P3** – Postup — přejmenování počítače a statické nastavení TCP/IPv4 (hodnoty, které jste zadali)

```text
DOPLNIT
```

<!-- nebo místo výpisu vložte screenshot (Ctrl+V) s viditelnými hodinami -->

- [ ] Hotovo

### M0-SRV2.P4 Aktivace

**M0-SRV2.P4** – Postup — jakým způsobem jste Windows aktivovali (při instalaci / v Settings / příkazem)

```text
DOPLNIT
```

<!-- nebo místo výpisu vložte screenshot (Ctrl+V) s viditelnými hodinami -->

- [ ] Hotovo

### M0-SRV2.P5 Jazyk, region, klávesnice, časové pásmo, home location

**M0-SRV2.P5** – Postup — co jste kde nastavili a na jaké hodnoty

```text
DOPLNIT
```

<!-- nebo místo výpisu vložte screenshot (Ctrl+V) s viditelnými hodinami -->

- [ ] Hotovo

### M0-SRV2.P6 Soukromí a telemetrie

**M0-SRV2.P6** – Postup — která nastavení soukromí jste změnili

```text
DOPLNIT
```

<!-- nebo místo výpisu vložte screenshot (Ctrl+V) s viditelnými hodinami -->

- [ ] Hotovo

### M0-SRV2.P7 PowerShell prompt s otiskem

**M0-SRV2.P7** – Postup — spuštění bloku pro nastavení promptu (vložte i jeho výstup / nové okno s promptem)

```text
DOPLNIT
```

<!-- nebo místo výpisu vložte screenshot (Ctrl+V) s viditelnými hodinami -->

- [ ] Hotovo

## PC1-WIN

> PC1-WIN připravujete až před Modulem 2 — tuto část vyplňte a odevzdejte znovu s Modulem 2.

### M0-PC1.P1 Vytvoření VM a instalace OS

**M0-PC1.P1** – Postup — parametry VM, zvolená edice a jazyk instalace

```text
DOPLNIT
```

<!-- nebo místo výpisu vložte screenshot (Ctrl+V) s viditelnými hodinami -->

- [ ] Hotovo

### M0-PC1.P2 OOBE bez Microsoft účtu, povolení účtu Administrator

**M0-PC1.P2** – Postup — jak jste obešli Microsoft účet, jak jste povolili vestavěný Administrator a co jste udělali s dočasným účtem

```text
DOPLNIT
```

<!-- nebo místo výpisu vložte screenshot (Ctrl+V) s viditelnými hodinami -->

- [ ] Hotovo

### M0-PC1.P3 Jméno počítače a síť

**M0-PC1.P3** – Postup — přejmenování počítače; nastavení síťové karty

```text
DOPLNIT
```

<!-- nebo místo výpisu vložte screenshot (Ctrl+V) s viditelnými hodinami -->

- [ ] Hotovo

### M0-PC1.P4 Aktivace

**M0-PC1.P4** – Postup — jakým způsobem jste Windows aktivovali

```text
DOPLNIT
```

<!-- nebo místo výpisu vložte screenshot (Ctrl+V) s viditelnými hodinami -->

- [ ] Hotovo

### M0-PC1.P5 Jazyk, region, klávesnice, časové pásmo, home location

**M0-PC1.P5** – Postup — co jste kde nastavili a na jaké hodnoty

```text
DOPLNIT
```

<!-- nebo místo výpisu vložte screenshot (Ctrl+V) s viditelnými hodinami -->

- [ ] Hotovo

### M0-PC1.P6 Soukromí a telemetrie

**M0-PC1.P6** – Postup — která nastavení soukromí jste změnili

```text
DOPLNIT
```

<!-- nebo místo výpisu vložte screenshot (Ctrl+V) s viditelnými hodinami -->

- [ ] Hotovo

### M0-PC1.P7 PowerShell prompt s otiskem

**M0-PC1.P7** – Postup — spuštění bloku pro nastavení promptu

```text
DOPLNIT
```

<!-- nebo místo výpisu vložte screenshot (Ctrl+V) s viditelnými hodinami -->

- [ ] Hotovo
