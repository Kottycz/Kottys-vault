---
aliases: [Windows, Windows NT, Windows NT architektura, Struktura Windows NT, MS-DOS a Windows 9x, Struktura MS-DOS]
tags: [os]
---

# WINDOWS (MS-DOS A WINDOWS NT)

## MS DOS A WINDOWS

Tři řady Windows:

- **MS-DOS + Windows** – DOS s grafickou nadstavbou Windows (Windows 1 až 3.x)
- **Windows s DOS jádrem** – DOS upravený a vložený jako jádro do Windows, které se tím staly samostatným OS (**Windows 95, 98, ME**)
- **Windows s NT jádrem** – úplně přepracované jádro, vlastně jiný typ OS (NT 3.x, NT 4, 2000, XP, Vista, 7, 8, 10 a serverové verze)

### MS DOS+WINDOWS

![[e7944b5c5d33b57f087bfcaa5e0b36ecdd01fd22896310a4ec1d681384a875e6.png]]

#### MS-DOS

**Jednoprocesorový, jednouživatelský, jednoúlohový** OS s jednoduchou **vrstvenou strukturou** (zdola nahoru):

- **BIOS** – základní ovládání hardwaru (klávesnice, monitor) přes hardwarová a softwarová přerušení; programátor vyvolá přerušení a tím komunikuje se zařízením
- **IO.sys** – obsluha periferií
- **MSDOS.SYS** – jádro (monolitické, jeden soubor); poskytuje další přerušení, např. přístup k souborům a grafice
- **COMMAND.COM** – textové rozhraní mezi uživatelem a systémem
  - obsahuje **vnitřní příkazy**
  - **vnější příkazy** jsou samostatné programy `.exe` / `.com`
- poslední vrstva – programy (vnější příkazy) a konfigurační soubory:
  - **CONFIG.SYS** – nastavení hardwaru (např. ovladač monitoru s českou znakovou sadou)
  - **AUTOEXEC.BAT** – nastavení softwaru (sekvence příkazů a programy po startu)

![[b96b2145b05ea27abbe84df81c1455504e1c10d0235a5d0eacb19775ab295e96.png]]

#### MS-DOS + WINDOWS

Spuštěním Windows 3.x v **rozšířeném módu** se změní horní část struktury:

- **WIN.COM** spouští Windows; Windows přidávají **multitasking**, 16bitové knihovny a od 3.11 for Workgroups základní síť peer-to-peer
- MS-DOS běží v **reálném módu** (paměť jen do 1 MB), Windows 3.x v **rozšířeném módu** (od i386) – rozšířená paměť a chráněný mód pro ochranu paměti
- ovladače I/O zařízení se spouští v souboru **SYSTEM.INI**
- **DOS EXTENDER** (**Win386.exe**) – podpora rozšířené paměti; obsahuje **VMM** (Virtual Machine Manager) pro souběh s DOS programy
- **VxD** – řadiče virtuálních zařízení, které VMM potřebuje pro I/O DOS programů
- **jádro Windows** (jádrem OS zůstává MSDOS.SYS) – správce prostředků, **3 soubory**:
  - **KRNL386.EXE** – správa paměti a procesů
  - **GDI.EXE** – grafický výstup (kurzor, ikony, písmo, tiskárna)
  - **USER.EXE** – prvky rozhraní mimo GDI (menu, okna, tlačítka)
- konfigurační soubory **.INI**: **WIN.INI** (software a uživatel), **SYSTEM.INI** (hardware)
- rozhraní k uživateli: **PROGMAN.EXE** (správce programů), **SHELL**, část **API** (knihovny `.DLL`)

==DOS programy== o jádru Windows ani .INI nevědí a počítají s tím, že jsou v systému samy → běží odděleně ve ==„virtuálních počítačích“==, které jim vytvoří iluzi výlučnosti a zabrání zásahům do cizích prostředků.

![[f7c37e99e742f1abb550cfa42045d9e78f1cf51a6f67a674ec336870b12a2066.png]]

### WINDOWS S DOS JÁDREM

![[f3b623e9c6d8af33eacebb1a0d748cec6290c467dbbc6ab10b6e20db389c8d47.png]]

#### Struktura Windows 9.x/Me

Od Windows 95 plnohodnotný OS se samostatným jádrem, **32bitový** (některé knihovny ještě 16bitové).

- spodní vrstva – **BIOS a ovladače**
- vrstva nad hardwarem (abstraktnější):
  - **VMM** – vytváří a udržuje virtuální počítače
  - **IFSM** – správa souborových systémů (FAT16, VFAT, FAT32, CDFS, UDF); přes něj se komunikuje s blokovými zařízeními
  - **Správce konfigurace** – ovladače hardwaru, Plug&Play
- **jádro – 3 moduly**, každý má knihovnu pro 16bit (`.exe`) a 32bit (`.dll`) aplikace:
  - **KERNEL** – multithreading, multitasking, správa paměti
  - **GDI** – grafická zařízení, grafický výstup, správce tisku, spooler
  - **USER** – uživatelské rozhraní, klávesnice, myš, okna, menu, ikony
- **REGISTR** – centrální konfigurační databáze (nahrazuje .INI, ty zůstaly kvůli kompatibilitě); soubory **SYSTEM.DAT** a **USER.DAT**

**Jak běží procesy:**

- **Win32** – společný virtuální stroj, každá aplikace vlastní paměťový prostor
- **Win16** – společný virtuální stroj i společný paměťový prostor
- **DOS** – každá aplikace vlastní virtuální stroj i paměťový prostor

![[a9bbf97ede353be060e830390328614ac762f786dce243b503388c26629110ff.png]]

### WINDOWS S NT JÁDREM

![[1085677959e5608792d9971ca116fdd25f8a08645dc08499a6e4afe14bc8dfbf.png]]

#### WINDOWS S NT JÁDREM DO VERZE XP

**NT (New Technology)** vznikalo nezávisle na DOSu, od začátku pro server a klienta v síti. Hlavní cíl: ==stabilita a zabezpečení==. Inspirace UNIXem.

- hlavní architekt přišel od firmy **DEC** (Digital), kde navrhoval **OpenVMS**
- NT je **víceprocesorový (SMP), víceuživatelský, víceúlohový, síťový** OS
- základní rozdělení: ==REŽIM JÁDRA== a ==UŽIVATELSKÝ REŽIM==

**Součásti:**

- **HAL** (Hardware Abstraction Layer) – rozhraní mezi hardwarem a zbytkem jádra
  - komunikuje s konkrétní platformou a vyšším vrstvám dává jednotné rozhraní
  - ovladače mluví s hardwarem jen přes HAL
  - soubor **HAL.DLL** – pro jinou platformu stačí ho vyměnit
- **KERNEL** (tvrdé jádro) a exekutiva – soubor **NTOSKRNL.EXE**
  - jeden soubor = monolitické jádro
  - obsluha přerušení, správa procesorů a procesů
  - další části se linkují z `.DLL` a `.SYS` = modulární struktura
- **proces SYSTEM** – obraz toho, co běží v jádru (kontejner pro vlákna jádra)
- **ovladače** – obecné moduly jádra: přístup k zařízením a sběrnicím, ale i filtry dat (komprese, šifrování)
- **IFSM** – správa souborových systémů (NTFS, FAT32, UDF), využívá ho správce I/O a cache
- **správce konfigurace** – Plug&Play a HotPlug, hlídá připojování zařízení
- **win32k.sys** – správa oken a grafiky běží v režimu jádra kvůli rychlosti
  - ==nevýhoda==: chyba v GUI může shodit systém (má přístup do paměti jádra), GUI se těžko vyměňuje
  - proto od Windows Server 2008 instalace **SERVER CORE** bez GUI
  - grafiku reprezentuje GDI, GDI+ a knihovny gdi*.dll
- **bezpečnostní subsystém** – **LSASS** ověřuje lokálně přihlášené uživatele a podle **SAM** v registru určuje oprávnění
- **SCM** (Service Control Manager, **services.exe**) – řídí služby; služby běží v uživatelském prostoru s vyššími oprávněními, bez vazby na uživatele
- komunikace s jádrem přes API:
  - **dokumentované** – USER32.DLL, GDI32.DLL…
  - **nedokumentované** – **NTDLL.DLL**, už přímo spouští systémová volání
- **podsystémy prostředí** – běh aplikací, které nejsou přímo pro NT (Win32 pro starší Windows a DOS, OS/2, POSIX); spouští se až s aplikací
  - DOS programy běží přes **ntvdm.exe** (NT Virtual DOS Machine)

**NT kombinuje víc architektur:**

1. ==MONOLITICKÁ== – jádro z jediného souboru NTOSKRNL.EXE
2. ==VRSTVENÁ== – rozdělení na uživatelský režim a režim jádra
3. ==MODULÁRNÍ== – moduly s definovaným rozhraním (správce procesů, paměti, I/O…)
4. ==KLIENT-SERVER== – knihovny API se chovají jako servery pro procesy, které je volají přes NTDLL.DLL

**Jak běží procesy:**

- **Win32** – společný virtuální stroj, každá vlastní paměťový prostor
- **DOS a Win16** – každá vlastní virtuální stroj i paměťový prostor
- **32bitové aplikace** na 64bit systému běží přes **WoW64** (Windows On Windows)

![[7a5868e2d6cee0f142c894d07987cb5c13f8eb0a76a2fa97a97857d9e8bc8e34.png]]

#### WINDOWS S NT JÁDREM OD VERZE VISTA A SERVER 2008

Rozdíly oproti předchozí verzi:

- modulární, přepracované jádro; **IPv6**; síť přesunuta do režimu jádra
- část GUI přesunuta do uživatelského režimu
- samostatný modul pro národní prostředí (ostatní moduly i opravy jsou na něm nezávislé)
- podpora **UEFI** (od Vista SP1)
- grafika na **WPF** (inspirace X-Window), **DWM** – správce oken
- **ASLR** – DLL knihovny se nahrávají na náhodné adresy (bezpečnost)
- **MinWin** (od Windows 7) – co nejmenší jádro, zbytek se dynamicky načítá paralelně → rychlejší start
- **XP Mode** – pro starší aplikace
- Windows 8: **Metro Apps** a **WinRT API**; Windows 10: **Universal Apps** a **UWP**
- **Windows Subsystem for Linux** – spouštění Linux aplikací
- **Nastavení** postupně nahrazuje Ovládací panely

![[2f34431b2a441078a128af8fcad834bddb0367c56095d0d5670abb2f0ab4838d.png]]

#### WINDOWS NT PODROBNĚJI

Většina pokročilých funkcí (souborové systémy, síť, správa paměti a procesů) běží v ==režimu jádra==. Všechny součásti jádra a ovladače sdílí **stejný virtuální adresový prostor**. V uživatelském režimu stačí jen pár procesů (služby, přihlášení).

![[f3d80ef1d0e5b94e8105a044d1a1c5b6b4fedb341055c596da4a85211a76e2c8.png]]

##### HAL

- cíl: snadno přenést Windows na jiný hardware → jádro je psané hlavně v **C**, jen malá část v Assembleru
- pro novou architekturu stačí přepsat části závislé na procesoru (přepínání kontextu, stránkovací tabulky, systémová volání)
- architektura je ve **vrstvách** – každá skrývá svá specifika a vyšším dává obecné rozhraní
- **HAL** je na ==nejnižší úrovni==, odstíní zbytek systému od hardwaru (různé procesory), poskytuje rutiny pro komunikaci se zařízeními; soubor **hal.dll**

##### TVRDÉ JÁDRO

Tenká vrstva nad HAL s jednoduchými mechanismy, ze kterých vyšší vrstvy staví složitější:

- **plánování vláken** na procesoru
- odložené volání procedur (**DPC**)
- **synchronizační primitiva** (event, spinlock, semafor, pushlock)
- práce s hardwarovými přerušeními
- část obsluhy systémových volání

##### OVLADAČE

- umožňují správci I/O komunikovat s hardwarem
- soubory formátu **PE** s koncovkou **.sys**

##### EXEKUTIVA

- staví na tvrdém jádru složitější mechanismy, které aplikace využívají nepřímo přes systémová volání
- skládá se z oddělených částí ve stejném adresovém prostoru, které spolu mluví jen přes ==přesně definovaná rozhraní== (podobné OOP)

![[9e2aa9d42dc408a203173254ffa7efc8c348b36d0fa0f236426088e9a24e938f.png]]

###### SPRÁVCE OBJEKTŮ (OBJECT MANAGER)

- jednotně vytváří a ruší objekty (otevřené soubory, klíče registru, mapované soubory) a řídí k nim přístup
- zapouzdřuje to, co platí pro všechny druhy objektů (alokace a uvolnění paměti)

###### SPRÁVCE PAMĚTI (MEMORY MANAGER)

- přiděluje rámce fyzické paměti, mapuje virtuální adresy na fyzické, obsluhuje výpadky stránky
- přiděluje a uvolňuje bloky virtuální paměti
- bezpečnost: **ASLR**

###### SPRÁVCE PROCESŮ (PROCESS MANAGER)

- spouštění, běh a ukončení procesů a vláken
- informace o procesech, změna priority, násilné ukončení

###### SPRÁVCE VSTUPNĚ/VÝSTUPNÍCH ZAŘÍZENÍ (I/O MANAGER)

- funkce kolem ovladačů a zařízení (fyzických i virtuálních)
- za běhu načítá a uvolňuje ovladače
- ovladače spolu komunikují přes objekty **zařízení (device)** – jako kanály mezi nimi

###### SPRÁVCE KONFIGURACÍ (CONFIGURATION MANAGER)

- ukládá nastavení systému do **registru** – na rozdíl od Unixu (textové soubory) v ==binární podobě==
- registr = malá databáze, rychlé hledání, méně místa; prohlíží se **regeditem**
- struktura jako adresáře: ==klíče== (= adresáře) a ==hodnoty== (= soubory); data mají jen hodnoty

**EDITOR REGISTRU**

![[af1aaecdb371b32182af05d3b8f6c5371a7b06009a33cbfdab67878bbcd3290b.png]]

###### BEZPEČNOSTNÍ MODEL

- každý smí dělat jen to, na co má oprávnění; admin určuje, k jakým objektům mají uživatelé přístup
- oprávnění jde nastavit nejen u souborů a klíčů registru, ale i u procesů, vláken, synchronizačních primitiv
- definuje i oprávnění k činnostem (vytvořit stránkovací soubor, načíst ovladač do jádra)

##### SUBSYSTÉMY

- vrstva knihoven nad **ntdll.dll** = prostředí pro aplikace; rozhraní je **dokumentované** a stabilní
- Windows mají **dva subsystémy**: ==Windows== a ==POSIX==
- POSIX umí vytvářet procesy přes **fork** (z Unixu), Windows ne; kvůli POSIXu má NTFS **hardlinky**

###### POSIX

- **Portable Operating System Interface** – standardy rozhraní unixových systémů, aby šly programy snadno přenášet
- Windows původně jen **POSIX 1**; od Vista / Server 2008 **SUA** (Subsystem for Unix-based Applications) – cca **2 000 funkcí** a **300 unixových programů**
- ==POSIX se spouští jen==, když je potřeba; subsystém Windows běží vždy
- konfigurace: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Subsystems`
- hlavní proces POSIXu **psxss.exe**, Windows **csrss.exe**; v jádru oba používají **win32k.sys**
- POSIX nemá vlastní ovladač ani knihovny – používá ty od subsystému Windows (jinak by byl kód zbytečně dvakrát a víc chyb)

###### WINDOWS

**Komponenty:**

- hlavní proces **csrss.exe** a jeho knihovny
- ovladač **win32k.sys** a ovladače grafiky
- knihovny, které překládají dokumentované Windows API na nativní volání **ntdll.dll**: kernel32.dll, user32.dll, gdi32.dll, advapi32.dll

**csrss.exe:**
- vykresluje okna konzolových aplikací, podporuje 16bitové DOS programy
- dozví se o každém spuštění a ukončení procesu nebo vlákna a drží si jejich seznam

**Proč je GUI v jádru (win32k.sys):**
- před NT 4 bylo GUI v csrss.exe (snaha o mikrojádro) → každé překreslení okna = přepnutí kontextu do csrss + systémové volání → pomalé
- od NT 4 je GUI v **win32k.sys** → méně přepínání a systémových volání
- win32k.sys spravuje okna, tlačítka, myš, klávesnici, kreslení; jako **HAL** skrývá rozdíly mezi grafickými kartami
- brána k němu: **gdi32.dll** (kreslení bodů, čar, křivek) a **user32.dll** (okna, menu, ikony)
- **kernel32.dll** – procesy, vlákna, paměť, synchronizace; **advapi32.dll** – služby a bezpečnost

###### REGISTR

![[2a7a088d496e4285ab6c9599c9bf160424fe8f8ff33abfd4aa11d98c92abe4b2.png]]

###### ZÁVISLOST SUBSYSTÉMU POSIX NA SUBSYSTÉMU WINDOWS

![[c11b1667ac0d818a31e5bfa6372be9fdfb5f043b53b8e35baab1965861a41c8c.png]]

##### SYSTÉMOVÉ PROCESY

I když je Windows **monolitický**, závisí na pár procesech, jejichž ukončení znamená ==restart počítače== – tzv. **systémové procesy**. Vidíš je ve Správci úloh (**Ctrl+Alt+Del**).

![[5b8c434a0c98691cdd501acd37e872fb463bc7fc902d8806f0388a7862242934.png]]

> [!warning] Pro hackery
> - Správce úloh nedovolí systémový proces ukončit („Přístup odepřen“).
> - Do Windows Vista ale tyto procesy nic nechránilo – Správce úloh má jen **natvrdo zakódované názvy** systémových procesů.
> - Toho může zneužít malware: pojmenuj program `winlogon.exe` a zkus ho ve Správci úloh ukončit.

###### NEČINNÉ PROCESY (SYSTEM IDLE PROCESS)

- **pseudoproces** – nemá soubor na disku ani DLL
- spotřebovává čas procesoru, když nikdo nemá co dělat
- vytvoří ho jádro na začátku startu
- ==PID== je vždy ==0==

###### PROCES SYSTEM

- nemá kód v uživatelském režimu ani `.exe`, ale běží v něm **pracovní vlákna (worker threads)** jádra
- čekají, až jim jádro nebo ovladač zadá práci – časově náročnou nebo takovou, kterou nejde udělat hned (dokončení obsluhy hardwaru, zápis „špinavých“ stránek na disk)
- pevné **PID** ==4== (před Windows 2000 bylo ==1==)

###### SPRÁVCE RELACÍ (SESSION MANAGER, SMSS.EXE)

- ==první proces== v uživatelském režimu, dokončí inicializaci systému
- vytváří **relace** – oddělené prostory uživatelů (každý může mít jinak namapované disky), číslují se
- **relace 0** (konzolová) – systémové procesy, služby a první přihlášený uživatel
- pro každou relaci spustí **winlogon.exe** (pro relaci 0 **wininit.exe**) a inicializuje **csrss.exe**
- hlídá csrss.exe a všechny winlogony – když některý spadne → modrá obrazovka `STATUS_CRITICAL_SYSTEM_PROCESS_DIED`

###### PROCESY PODÍLEJÍCÍ SE NA PŘIHLÁŠENÍ (WINLOGON.EXE, LSASS.EXE)

**winlogon.exe** – grafické přihlášení uživatele:

- metody ověření jsou v samostatných DLL (nejčastěji jméno a heslo)
- ==ochrana proti keyloggerům==: před přihlášením se může vyžadovat **Ctrl+Alt+Del**; tuhle kombinaci zachytí a pohltí okno **SAS Window**, takže keylogger (pokud není v jádru nebo ve winlogonu) nepozná, kdy se zadává heslo
- zadané údaje pošle **lsass.exe** k ověření
- běží i po přihlášení – zajišťuje odhlášení a reaguje na Ctrl+Alt+Del (dialog nebo rovnou Správce úloh)

**lsass.exe** – ověří jméno a heslo a vytvoří **token** (objekt, kterým uživatel prokazuje oprávnění):

- admin se zapnutým **UAC** dostane ==dva tokeny==:
  - plný se všemi oprávněními
  - omezený – používá se pro běžné aplikace a inicializaci prostředí
- program, který potřebuje admin práva, se může zeptat (UAC) a pak dostane plný token

**Inicializace prostředí po přihlášení:**

- winlogon spustí procesy z hodnoty **Userinit** v `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon`
- **userinit.exe** spustí přihlašovací skripty a předá řízení shellu z hodnoty **Shell**
- výchozí shell = **Průzkumník (explorer.exe)** – plocha, procházení složek, spouštění programů

**PŘIHLAŠOVACÍ OBRAZOVKA**

![[4eb84a308f44c47665b1119b0fa6d9375998fff79aeb0269500a19e31c80e78f.png]]

**VÝZVA KE STISKU AKTIVAČNÍ KOMBINACE KLÁVES**

![[2e1563bf79f72e28af6101c4c249e7cb7a6fdf4efe8634289d2adbeb7b18982b.png]]

**DIALOG WINLOGON**

![[6b7fa5477c79daf85ca99990fb51da73f92a81756e818fab611f9e75495e6e35.png]]

> [!warning] Pro hackery
> - V hodnotě Userinit má být jen `userinit.exe` ze systémové složky.
> - Jsou-li tam další procesy, jde pravděpodobně o malware.

###### PROCESY PRO PODPORU SLUŽEB (SERVICES.EXE, SVCHOST.EXE)

- **služby** = programy na pozadí bez interakce s uživatelem, běží i bez přihlášení
- **SCM** (**services.exe**) je instaluje, spouští, zastavuje a posílá jim příkazy (ovladače jádra řadí mezi služby, ale moc se o ně nestará)
- služba = soubor **PE** `.exe` s kódem pro komunikaci se SCM
- víc služeb může sdílet jeden proces → **svchost.exe** je „hostí“
- správa: **services.msc**; konfigurace v `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services`

**SLUŽBY**

![[c32c8077b73ebb39e9aa65ef86428af4063793647be2aa29e64c35e442aa2a34.png]]

**NASTAVENÍ SLUŽBY TCPIP V REGISTRU**

| Hodnota | Význam |
| :-- | :-- |
| **Description**, **DisplayName** | jen informativní, sloupce Název a Popis v services.msc |
| **ErrorControl** | co udělat při chybě spuštění |
| **ImagePath** | soubor služby (bez ní `X.exe` / `X.sys` v systémové složce) |
| **Start** | kdy se služba spustí |
| **Type** | služba v uživatelském režimu, nebo ovladač jádra |
| **Tag** | pořadí ovladače ve skupině |

- služby jde řadit do **skupin**; pořadí skupin je v `...\Control\ServiceGroupOrder`, pořadí ve skupině podle tagu v `...\Control\GroupOrderList`
- **závislosti** – služba běží jen, když běží služby (nebo aspoň jedna ze skupiny), na kterých závisí; např. Zvuk systému Windows potřebuje Windows Audio, RPC a Plánovač multimédií

![[e361a865ed678a5f0ca967900c5c712b551514c20f55a79028e4a2cbbaea60a8.png]]

**ERROR**

![[63d4edcb9c60fafe2eb818e43a8ec401d1c3c7bba994982fd995be14585f9979.png]]

**START**

![[8d610b25c4cbec28d83cb04e2a297b5dbff4fab7c17418ab4942336105e3f937.png]]

**TYPE**

![[793d867f7298f742d244b243aec1f4dac96c1215af3ee3714dfc844c0490959b.png]]

#### SERVEROVÉ EDICE

Stejné jádro jako desktopové edice + další nástroje (**DHCP server, DNS Server, Active Directory**…).

![[6ec1a6fb8def4315e0d84f3de39c75061b414bed4ab5b82fa28a5114fd34da0e.png]]

---

**Struktura OS:** [[01_STRUKTURA_OPERAČNÍCH_SYSTÉMŮ|Architektury OS]] · [[01a_Windows|Windows]] · [[01b_Unix|UNIX]] · [[01c_Linux|Linux]] · [[01d_Apple|Apple]] · [[01e_Android|Android]]
