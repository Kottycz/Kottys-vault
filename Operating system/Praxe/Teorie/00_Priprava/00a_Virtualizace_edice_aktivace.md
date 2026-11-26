---
aliases: [Příprava prostředí, Virtualizace a edice Windows]
tags: [ops, teorie]
---

# Příprava prostředí – virtualizace, edice, aktivace

Než ve škole spustíme první službu, potřebujeme stroje, na kterých poběží. Všechny tři musí mít **stejný základ** – jinak se chyby (jiné jméno, jiné heslo, špatný čas) projeví až o několik modulů později a těžko se hledají. Tahle poznámka řeší, **na čem** stroje běží, **jaký Windows** mají a **jak se aktivuje**.
Praxe: [[00_Priprava_OS]] · Další: [[00b_Identita_a_sit]] · [[00c_Cas_jazyk_soukromi]]

---

## Virtualizace

Kdybychom chtěli doménu, [[DHCP]] a soubory zkoušet na skutečných serverech, potřebovali bychom několik fyzických počítačů, kabely a místo. **Virtualizace** umožní spustit víc „počítačů“ na jednom fyzickém.

- **[[hypervizor]]** je software, který rozdělí hardware hostitele ([[CPU]], [[RAM]], disky, síť) mezi **[[VM|virtuální stroje]]** a odděluje je od sebe
- každá [[VM]] má vlastní operační systém a o ostatních neví, i když sdílí stejný hardware
- virtuální síť umožní, aby se stroje „viděly“ jako v jedné místnosti na jednom switchi – přesně to potřebujeme pro síť `192.168.N.0/24`

### Typy hypervizorů

| Typ | Kde běží | Příklady | Použití |
| :-- | :-- | :-- | :-- |
| **typ 1 (bare-metal)** | přímo na hardwaru, bez [[operační systém\|OS]] pod sebou | Hyper-V, VMware ESXi, Proxmox, KVM | servery, produkce |
| **typ 2 (hostovaný)** | jako aplikace v běžném [[operační systém\|OS]] | VirtualBox, VMware Workstation | výuka, testy na notebooku |

Typ 1 je rychlejší, protože mezi ním a hardwarem nic není. Typ 2 je pohodlný, protože ho spustíš jako program. Pro projekt nezáleží, který škola používá – důležité jsou parametry strojů.

### Proč se virtualizuje i ve firmách

- **využití hardwaru** – jeden výkonný server nahradí desítky málo vytížených
- **rychlé zřízení a obnova** – nový stroj je za minuty, při chybě se vrátíš ke snapshotu
- **izolace** – chyba na jednom stroji neovlivní ostatní
- **přenositelnost** – virtuální disk jde zkopírovat na jiného hostitele
- **nevýhoda:** spadne hostitel → spadnou **všechny** [[VM]] na něm. Ve větších firmách se proto [[VM]] rozkládají na víc hostitelů (cluster)

### Zdroje VM

| | SRV1-DC | SRV2-FS | PC1-WIN |
| :-- | :-- | :-- | :-- |
| [[VM\|vCPU]] / [[RAM]] | 2 / 8 GB | 2 / 8 GB | 2 / 8 GB |
| systémový disk | 100 GB | 100 GB | 60 GB |
| další disky | – | 5× 5 GB | – |

- 2 jádra na výukové služby stačí, víc by zbytečně bralo hostiteli
- 8 GB [[RAM]] – Windows Server s [[GUI]] a rolemi i Windows 11 potřebují kolem 4 GB, zbytek je rezerva
- 5 disků na SRV2-FS je pro **Storage Pool** a simulaci výpadku disku v Modulu 6; přidávají se hned, protože disk se snáz přidá vypnutému stroji
- **[[VM|vCPU]]** = virtuální jádro, **virtuální disk** = soubor na hostiteli (`.vhdx`); *thin provisioned* disk zabírá na hostiteli jen skutečně využité místo, i když se tváří jako 100 GB

### Snapshot není záloha

**[[snapshot]]** si zapamatuje stav stroje v jednom okamžiku a můžeš se k němu vrátit – hodí se před rizikovou změnou (instalace role). Zálohou ale není:

- leží na **stejném hostiteli** jako stroj → když hostitel odejde, přijdeš o obojí
- dlouhá řada snapshotů zpomaluje disk a zabírá místo
- návrat vrátí **všechno**, takže zahodíš i dobrou práci po snapshotu
- **řadič domény** se snapshotem nevrací: [[AD DS|AD]] si pamatuje pořadí změn, a když „skočí v čase“, ostatní řadiče ho odmítnou (**[[USN rollback]]**). Řadič se zálohuje přes *System State*

## Edice Windows Serveru

Windows Server se prodává v edicích, které se liší funkcemi, licencí a cenou.

| | **Standard** | **Datacenter** |
| :-- | :-- | :-- |
| nasazení | fyzické servery, málo [[VM]] | hodně [[VM]], cloud, hyperkonvergence |
| [[VM]] na jednu licenci | 2 | neomezeně |
| funkce | základní sada rolí | navíc Storage Spaces Direct, Shielded VMs, rozšířená Storage Replica |
| cena | nižší | vyšší |

- licencuje se **podle počtu jader** hostitele (min. 16 na server) a k tomu **[[CAL]]** – licence pro uživatele nebo zařízení, které k serveru přistupují
- malé škole by stačil **Standard**; my používáme **Datacenter**, aby se žádná probíraná funkce (např. Storage Spaces v Modulu 6) nezastavila na licenci

### Desktop Experience × Server Core

| | **Desktop Experience** | **[[Server Core]]** |
| :-- | :-- | :-- |
| [[GUI]] | ano (Server Manager, konzole [[MMC]]) | ne, jen PowerShell, `sconfig` |
| nároky | vyšší | nižší |
| útočná plocha | větší (víc součástí = víc zranitelností a aktualizací) | menší |
| správa | lokálně i vzdáleně | hlavně vzdáleně (PowerShell, Server Manager, Windows Admin Center) |
| typicky | výuka, menší firmy | produkční řadiče domény, souborové servery |

- v praxi se pro produkční řadiče často doporučuje **Server Core** (bezpečnější)
- my volíme **Desktop Experience** – chceme se naučit grafické konzole (Server Manager, [[ADUC]], [[DNS]] Manager, [[DHCP]]) a vidět, co který krok dělá; každý modul má postup v [[GUI]] i v PowerShellu

## Licence a aktivace

Instalace a aktivace jsou dvě různé věci. **Neaktivovaný Windows** běží jen omezenou dobu, pak se objeví vodoznak a některé funkce se omezí. Jak se aktivuje, záleží na licenci:

| Způsob | Jak funguje | Kde |
| :-- | :-- | :-- |
| **Retail / [[KMS\|OEM]]** | jeden klíč = jeden stroj, ověřuje Microsoft | domácnosti, malé firmy |
| **[[KMS\|MAK]]** | jeden klíč pro víc strojů, omezený počet aktivací, ověřuje Microsoft | střední nasazení |
| **[[KMS]]** | licenční server ve vlastní síti, stroje se aktivují samy; aktivace platí ~180 dní a obnovuje se | školy, firmy s mnoha stroji |
| **[[KMS\|AVMA]]** | [[VM]] se aktivují podle licence Datacenter hostitele | virtualizace |

- [[KMS]]: když stroj dlouho nevidí licenční server, aktivace vyprší – proto se musí obnovovat
- škola používá **[[LAB KEY]]** – hromadný laboratorní klíč pro výuku
  - zadat **při instalaci** (obrazovka *Product Key*), nebo **po instalaci** v Settings → System → Activation → Change product key, nebo příkazy `slmgr.vbs /ipk <klíč>` a `slmgr.vbs /ato`
  - stav: Settings → System → Activation, nebo `slmgr.vbs /xpr` (vypíše trvalou aktivaci nebo datum vypršení)
- klíč je citlivý údaj → do dokumentace ani na screenshot nikdy, nahradit `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`

## Windows 11 Education N

PC1-WIN je školní stanice, proto **Windows 11 Education N**:

- **Education** – edice pro školy, má funkce Enterprise (připojení do domény, centrální správa přes [[GPO]]), liší se licencí
- **N** – varianta bez mediálních technologií (Media Player, kamera…), vznikla na základě rozhodnutí EU; jinak funkčně stejná a chybějící součásti jdou doinstalovat

### Problém s Microsoft účtem

Windows 11 při instalaci ([[OOBE]]) tlačí přihlášení **Microsoft účtem**, když vidí síť. Na školním PC je to špatně:

- osobní účet žáka/učitele by řídil přihlašování na školním PC → správa a hesla mimo kontrolu školy
- nejde založit lokální účet jménem `Administrator` – to jméno patří vestavěnému účtu, který je vypnutý

Řešení (běžné i v praxi):

1. během [[OOBE]] **odpojit síť** a zvolit *Continue with limited setup*, nebo instalaci předem připravit souborem odpovědí `autounattend.xml`
2. založit **dočasný lokální účet**
3. po instalaci zapnout vestavěný účet: `net user administrator /active:yes` a dočasný účet smazat

Stejně se připravují **golden image** pro velká nasazení, kde se stroje nemají hlásit pod osobními účty.

## U nás

- 3 [[VM]]: **SRV1-DC** (budoucí řadič domény), **SRV2-FS** (souborový server), **PC1-WIN** (klient)
- servery **Windows Server 2025 Datacenter s Desktop Experience**, klient **Windows 11 Education N**
- všechny aktivované [[LAB KEY]], všude vestavěný `Administrator`, žádný Microsoft účet
