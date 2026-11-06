---
aliases: [Windows, Windows NT, Windows NT architektura, Struktura Windows NT, MS-DOS a Windows 9x, Struktura MS-DOS]
tags: [os]
---

# WINDOWS (MS-DOS A WINDOWS NT)

## MS DOS A WINDOWS

Řada **MS-DOS + Windows** zahrnuje operační systém DOS s grafickou nadstavbou Windows. Jedná se o verze od Windows 1 až do verze Windows 3.x Řada **Windows s DOS jádrem** vznikla úpravou původního samostatného operačního systému MS-DOS a jeho včleněním jako jádra do Windows, které se tímto staly samostatným operačním systémem. Tato řada zahrnuje **Windows 95, 98 a ME**.

- **Windows s NT jádrem** mají zcela přepracované jádro a přes značnou kompatibilitu se vlastně jedná o jiný typ operačního systému. Patří zde Windows NT 3.x, Windows NT 4.x, Windows 2000, Windows XP, Windows Vista, Windows 7, Windows 8, Windows 10, Windows NT Server, Windows 2000 Server, Windows 2008 Server, Windows 2012 Server, Windows 2016 Server.

### MS DOS+WINDOWS

![[e7944b5c5d33b57f087bfcaa5e0b36ecdd01fd22896310a4ec1d681384a875e6.png]]

#### MS-DOS

MS-DOS je **jednoprocesorový, jednouživatelský, jednoúlohový** operační systém. Samotný DOS bez spuštěné nástavby Windows má velmi jednoduchou **vrstvenou strukturu**. Nejblíže hardwaru je **BIOS** a dále soubor **IO.sys**, který se stará o obsluhu periferií.hardwaru (například klávesnice, monitoru BIOS poskytuje programátorům základní ovládání hardwaru (například klávesnice, monitoru) přes hardwarová a softwarová přerušení.

Pokud programátor potřebuje komunikovat s určitým zařízením, vyvolá příslušné přerušení (k tomu jsou v programovacích jazycích speciální příkazy). Nad vrstvou ovládání hardware je vrstva samotného jádra systému představovaná souborem **MSDOS.SYS**. MS-DOS má tedy monolitické jádro složené z jediného souboru. Jádro poskytuje další softwarová přerušení, například pro přístup k souborům nebo práci s grafikou.

Následující vrstva, tvořená souborem **COMMAND.COM** je textové rozhraní mezi uživatelem a systémem. Uživatel zadává příkazy a rozhraní na ně reaguje a vypisuje výsledky nebo chybová hlášení. Samotný COMMAND.COM obsahuje sadu **vnitřních příkazů**. Ostatní příkazy se nazývají **vnější příkazy** a jsou implementovány jako programy s příponou .exe nebo .com.

- V podlední vrstvě pak běží programy představující vnější příkazy a patří sem také konfigurační soubory:
  - **CONFIG.SYS** pro nastavení hardwaru (například spuštění ovladače monitoru s českou znakovou sadou)
  - **AUTOEXEC.BAT** pro nastavení softwaru (například spuštění sekvence vnitřních a vnějších příkazů a spuštění programu po startu systému.

![[b96b2145b05ea27abbe84df81c1455504e1c10d0235a5d0eacb19775ab295e96.png]]

#### MS-DOS + WINDOWS

Když v MS-DOS 6.22 spustíme windows 3.x v **rozšířeném módu**, struktura celého systému se v horní části změní. Na obrázku je spodní část trochu shrnura (BIOS, MSDOS.SYS). K nim je přidán soubor **WIN.COM**, který slouží ke spuštění celých Windows a dále ovladače. Windows přidávají **multitasking**, 16bitové knihovny a ve verzi Windows 3.11 for Workgroups základní podporu sítě peer-to-peer.

Zatímco MS-DOS pracuje v **reálném módu**, kdy lze využít paměť pouze do 1MB. Windows 3.x pracují v **rozšířeném módu**, dostupném až od procesorů i386, kde lze kromě rozšířené paměti využívat také chráněný mód procesoru pro ochranu paměti. Řadiče (ovladače, drivery) ovládají I/O zařízení pro Windows. Jsou spouštěny v souboru SYSTÉM.INI.

- **DOS EXTENDER** je modul pro podporu využití rozšířené paměti (Extended Memory). Je představován souborem **Win386.exe**.

Součástí tohoto souboru je také **Správce virtuálních zařízení (VMM = Virtual Machine Manager)**, který ovládá možnosti Windows pro souběh s programy DOS.

- **Řadiče virtuálních zařízení (VxD)** jsou řadiče, které VMM potřebuje pro manipulaci s I/O zařízeními pro programy DOS v rozšířeném módu.
- V další vrstvě je jádro Windows (jádrem OS zústává MSDOS.SYS), které funguje jako správce prostředků vzhledem k programům běžícím pod Windows (i DOS programům spuštěným z Windows). Skládá se ze **3 souborů**:
  - **KRNL386.EXE** – správce paměti, správce procesů
  - **GDI.EXE** – grafické rozhraní (kurzor, ikony, písmo, …), cokoli co souvisí se základními funkcemi pro grafický výstup na obrazovku, tiskárnu, apod.
  - **USER.EXE** – prvky uživatelského rozhraní, které nepatří do GDI (menu, okna, tlačítka, …)
- V další vrstvě najdeme konfigurační soubory s příponou **.INI**.
  - **WIN.INI** – konfigurace software a uživatelské nastavení.
  - **SYSTÉM.INI** – konfigurace hardware.

Následuje vrstva, která je rozhraním mezi uživatelem, programy a samotným systémem. Soubor **PROGMAN.EXE** je správce programů, **SHELL** je grafické a textové rozhraní mezi uživatelem a systémem. Zde bychom také mohli zařadit část **API** rozhraní (Application Programming Interface) reprezentovaného dynamicky linkovanými knihovnami.

Většina knihoven má příponu .DLL, některé mají příponu .exe, přípona knihoven fontů závisí na typu fontů (např. ttf pro true type fonty). ==DOS programy== nevědí nic o existenci jádra windows a ini souborů, proto horní „Windows“ vrstvy nevyužívají. DOS programy jsou napsány pro jednouživatelský, jednoúlohový systém DOS, bez jakýchkoliv ohledů na možnost sdílení prostředků s jinými procesy.

Proto je nutné je separovat do ==„virtuálních počítačů“==, které programům vytvoří iluzi výlučné existence v systému a znemožní jim zásahy do prostředků jiných procesů.

![[f7c37e99e742f1abb550cfa42045d9e78f1cf51a6f67a674ec336870b12a2066.png]]

### WINDOWS S DOS JÁDREM

![[f3b623e9c6d8af33eacebb1a0d748cec6290c467dbbc6ab10b6e20db389c8d47.png]]

#### Struktura Windows 9.x/Me

Od verze 4.x (Windows 95) jsou Windows již plnohodnotným operačním systémem se samostatným jádrem. Je to **32birový systém** (ale některé knihovny zůstávají 16bitové). Spodní vrstva (BIOS a ovladače) slouží k přístupu systému k zařízením.

- Následující vrstva se také vztahuje k hardwaru, ale již na abstraktnější úrovni. Skládá se z následujících modulů:
  - **VMM** – Virtual Machine Manager, vytváří a udržuje prostředí virtuálních počítačů.
  - **IFSM** – Installable File Systems Manager, spravuje různé typy souborových systémů, FAT16, VFAT, FAT32, CDFS, UDF, atd. Přes IFSM se komunikuje s paměťovými zařízeními typu mass storage (blokové zařízení).
  - **Správce konfigurace** – spravuje ovladače hardware, včetně funkce Plug&Play.
- Jádro se skládá ze **tří modulů**, každý z nich má dvě dynamicky linkované knihovny (jednu pro 16bitové aplikace s příponou .exe, druhou pro 32bitové aplikace s příponou .dll:
  - **KERNEL** – multithreading, multitasking, správa paměti,
  - **GDI** (Graphics Device Interface) – rozhraní grafických zařízení (obrazovka, tiskárna, plotter, …), grafický výstup, správce tisku, spooler.
  - **USER** – uživatelské rozhraní, vstupy z klávesnice, myši, výstupy do GUI, okna, menu, ikony.
  - **REGISTR (Windows Registry)** – centrální konfigurační databáze systému. Najdeme zde většinu z toho, co v předchozích verzích bylo v .INI souborech (ty jsou i v této verzi zachovány z důvodů zpětné kompatibility). Registr je uložen v souborech SYSTÉM.DAT a USER.DAT

**Jak běží procesy:**

- **Win32 aplikace** běží všechny ve společném virtuálním stroji, každá ve svém vlastním paměťovém prostoru.
- **Win16 aplikace** běží ve společném virtuálním stroji a sdílejí jeden společný paměťový prostor.
- **DOS aplikace** beží každá ve svém vlastním virtuálním stroji, v něm má svůj vlastní paměťový prostor.

![[a9bbf97ede353be060e830390328614ac762f786dce243b503388c26629110ff.png]]

### WINDOWS S NT JÁDREM

![[1085677959e5608792d9971ca116fdd25f8a08645dc08499a6e4afe14bc8dfbf.png]]

#### WINDOWS S NT JÁDREM DO VERZE XP

Jádro systému **Windows NT (New Technology)** vznikalo nezávisle na systému MS-DOS. Už při jeho návrhu bylo projektováno pro typické použití tohoto systému jako serveru nebo klienta v síti (Windows NT Server, Windows NT Workstation). Hlavním hlediskem při návrhu NT je ==stabilita a možnost zabezpečení==.

- Na celém konceptu je vidět inspirace UNIX systémy.

Hlavním architektem NT byl XXXXXXX, architekt UNIX systému OPEN VMS, kterého Microsoft „přetáhl“ ze společnosti DIGITAL (DEC = Digital Equipment Corporation, která v té době byla technologickým leadrem například v oblasti mikroprocesorů, se svými 64bitovými procesory Alpha. Digital byl později pohlcen společností COMPAQ a ta společností Hewlett Packard). Windows NT jsou **víceprocesorový (SMP – symetrický multiprocessing), víceuživatelský, víceúlohový, síťový** operační systém.

- Zjednodušení struktura systému je na obrázku.

Důležité je především rozdělení do dvou základních režimů – ==REŽIM JÁDRA== (privilegovaný režim) a ==UŽIVATELSKÝ REŽIM==.

- **HAL** – Hardware Abstraction Layer – vrstva abstrakce hardware je rozhraní mezi hardwarem a zbytkem jádra systému a zajišťuje „nezávislost“ na hardwarové platformě.
  - Na jedné straně zajišťuje komunikaci s konkrétní ardwarovou platformou a na druhé straně unifikované rozraní pro další vrstvy operačního systému.
  - Ovladače komunikují s hardwarem pouze sprostředkovaně přes tuto vrstvu.
  - Načítá se ze souboru **HAL.DLL** a je oddělena od ostatních částí systému – právě z důvodu přenositelnosti mezi hardwarovými platformami (stačí vyměnit soubor HAL.DLL).
- **KERNEL** (tvrdé jádro) a exekutiva jsou fyzicky uloženy v souboru **NTOSKRNL.EXE**.
  - Jediný soubor, tedy monolitické jádro.
  - Kernel zachytává a obsluhuje přerušení, provádí správu procesorů, procesů, a podobně.
  - Ostatní součásti jádra jsou k jádru linkovány z dynamických knihoven (soubory .DLL) nebo modulů (soubory .SYS) – tedy modulární struktura jádra.
- **HLAVNÍ SYSTÉMOVÝ PROCES** – v aplikaci pro správu procesů je vidět pod názvem **SYSTEM**, je obrazem toho co běží v jádru. Jedná se o kontejner pro prováděcí vlákna jádra.
- **OVLADAČE** nesouvisejí jen se zařízeními, jsou obecné, jedná se o moduly jádra, které mohou sloužit jak pro přístup k zařízením, sběrnicím a podobně, ale mohou to být také filtry, přes které procházejí data (komprimace, šifrování, třídění, …).

Nad ovladači souborovýc systémů je systém pro jejich správu **IFSM**, který zajišťuje přístup k předem určeným souborovým systémům (NTFS, FAT32, UDF, atd.). Je využíván správcem I/O a vyrovnávací paměti.

- **SPRÁVCE KONFIGURACE** například zajišťuje funkce Plug&Play a HotPlug. Neustále sleduje stav sběrnice a hlídá připojování zařízení, u nových provádí instalační proceduru.
- Moduly pro správu oken a grafiky beží v režimu jádra, z důvodu urychlení práce aplikací. Tato část jádra se načítá ze souboru **win32k.sys**.
  - ==Nevýhodou== umístění grafického rozhraní do režimu jádra je bezpečnostní riziko, riziko porušení stability systému v případě chybových stavů tohoto modulu (pracuje v režimu jádra = má přístup do paměti systémových procesů).
  - Další nevýhodou je náročnost výměny grafického rozhraní za alternativní.
  - Ve Windows Server od verze 2008 je možnost instalovat systém bez GUI a bez dalších součástí, které GUI vyžadují – instalace **SERVER CORE**.
  - Grafické rozhraní je reprezentováno modulem GDI, GDI+ a dynamicky linkovanými knihovnami gdi*.dll
- **Bezpečnostní subsystém** souvisí především s modulem **LSASS** (Local Security Authority SubSystem). Provádí autentizaci uživatelů, kteří se přilašují lokálně a podle databáze v klíči registru **SAM** určují přístupová oprávnění.
- **SCM** (Service Control Manager), správce služeb, načítaný ze souboru **services.exe**, zajišťuje běh služeb a komunikaci s nimi. Samostné služby běží v uživatelském prostoru, ale s vyššími oprávněními a bez vazby na konkrétního uživatele (v kontextu nějakého systémového účtu).
- Komunikace procesů s jádrem probíhá pomocí volání funkcí nebo procedur dokumentovaných rozhraní (**dokumentovaná API**) nebo nedokumentovaných rozhraní (**nedokumentovaná API**), které pak spustí systémová volání v režimu jádra, která jsou jádrem obsloužena.
  - Dokumentovaná rozhraní jsou objekty v systémových knihovnách **USER32.DLL, GDI32.DLL** a další.
  - Nedokumentované API je v souboru **NTDLL.DLL** a může již přímo spouštět systémová volání.
- **Podsystémy prostředí** jsou rozhraní zajišťující správný běh různých typů procesů.
  - Běží v nich aplikace, které nemusí být kompatibilní s Windows NT.
  - Jedná se o podsystém pro aplikace psané pro starší verze Windows a DOS (WIN32), podsystém pro OS/2, POSIX, atd.
  - Tyto podsystémy jsou spouštěny až při spuštění aplikace patřící danému podsystému.

Součástí podsystému Win32/Windows je mechanismus virtuálních počítačů. Běh virtuálních počítačů je spuštěn aplikací v souboru **ntvdm.exe** (NT Virtual DOS Machine).

**Jak je vidět z obrázku, Windows NT kombinují více různých architektur pro své různé části:**

1. Jádro je generováno z jediného souboru NTOSKRNL.EXE, je ==MONOLITICKÉ==.
2. ==VRSTVENÁ== architektura se uplatňuje v rozdělení na uživatelský režim a režim jádra.
3. ==MODULÁRNÍ== architektura se uplatňuje v připojování uzavřených modulů, které poskytují služby přes nadefinované rozhraní a komunikace probíhá volně mezi různými moduly (správce procesů, správce paměti, I/O, správce ovladačů).
4. Architektura ==KLIENT-SERVER== se uplatňuje v API, což je sada dynamicky linkovaných knihoven, které se chovají jako servery (poskytují služby) pro procesy z vyšších vrstev systému (klienti), kteří přes knihovnu NTDLL.DLL tyto služby využívají.

**Jak běží procesy:**

- **Win32 aplikace** beží všechny ve společném virtuálním stroji, každá má svůj vlastní paměťový prostor.
- **DOS a Win16 aplikace** mají každá svůj vlastní virtuální stroj a v rámci tohoto stroje svůj vlastní paměťový prostor.
- **32bitové aplikace** běží v prostředí **WoW64** (Windows On Windows), které je překládá na 64bitové.

![[7a5868e2d6cee0f142c894d07987cb5c13f8eb0a76a2fa97a97857d9e8bc8e34.png]]

#### WINDOWS S NT JÁDREM OD VERZE VISTA A SERVER 2008

**Popíšeme jen rozdíly oproti předchozí verzi:**

- Modulární, zcela přepracované jádro
- IPv6
- Podpora sítě přesunita do režimu jádra

Část implementace GUI přesunuto do uživatelského režimu.

- Samostatný modul pro národní prostředí.

Ostatní moduly (= i opravné balíčky) jsou nezávislé na národním prostředí.

- Podpora **UEFI** - od Vista SP1

Grafické prostředí na **WPF** (Windows Presentation Foundation) - Grafický podsystém inspirovaný X-Windows ze světa UNIXu.

- **DWM** - Desktop Windows Manager - správce oken.
- **ASLR** - Adress Space Load Randomisation - DLL knihovny se do paměti nahrávají na náhodné adresy (bezpečnostní opatření).
- **MinWin** (od Windows 7) - co nejmenší základní jádro a vše ostatní, co běží v režimu jádra jsou dynamicky připojované moduly - rychlejší start systému (po načtení tvrdého jádra je již možné pracovat a ostatní části systému se načítají paralelně).
- **XP Mode** - pro spouštění starších aplikací.

Od Windows 8 **METRO APPS** a nový grafický subsystém **WinRT API** Od Windows 10 **UNIVERSAL APPS** a nový grafický subsystém **Universal Windows Platform**.

- **Windows Subsystem for Linux** - součást jádra, umožňuje spouštět LINUX aplikace.

Nástroj **NASTAVENÍ** - postupně nahradí Ovládací Panely.

![[2f34431b2a441078a128af8fcad834bddb0367c56095d0d5670abb2f0ab4838d.png]]

#### WINDOWS NT PODROBNĚJI

Většina pokročilých funkcí Windows NT (souborové systémy, síťová komunikace, správa paměti a procesů) běží v ==režimu jádra==. Systém pro svoji plnohodnotnou činnost vyžaduje běh pouze několika málo procesů, které zajišťují správu služeb či dovolují přihlášení uživatele přes grafické rozhraní. Všechny součásti jádra a ovladače zařízení sdílí stejný virtuální adresový prostor.

![[f3d80ef1d0e5b94e8105a044d1a1c5b6b4fedb341055c596da4a85211a76e2c8.png]]

##### HAL

Windows jsou psány tak, aby nebylo obtížné upravit celý systém pro běh na dalších platformách – například na nových procesorech či základních deskách.

- **Přenositelnost** patří mezi důvody, proč je celé jádro naprogramováno převážně v jazyce **C**, kterému někteří přezdívají „přenositelný Assembler“.

Pouze velmi malou část kódu psali vývojáři v Assembleru, jazyku striktně závislém na konkrétním procesoru či rodině procesorů. Pro přenesení Windows na novu architekturu tedy stačí přepsat některé části jádra a systémových knihoven DLL, které zapouzdřují mechanismy, jejichž implementace závisí na konkrétním druhu procesoru (přepínání kontextu vláken, obsluha stránkovacích tabulek, systémová volání). Jedním z cílů při navrhování nového operačního systému bezesporu je usnadnit programátorům psaní aplikací a ovladačů.

Programátoři běžných aplikací by například neměli řešit odlišnosti různých typů procesorů. To platí i o většině ovladačů jádra. Z tohoto důvodu se architektura Windows dělí do několika vrstev. Každá vrstva v sobě skrývá některé specifické vlastnosti a problémy a vrstvám vyšší úrovně poskytuje obecná rozhraní.

- **HAL** se v architektuře Windows nachází na ==nejnižší úrovni== a jejím úkolem je odstínit ostatní části operačního systému a aplikace od specifik hardware, jako jsou různé modely procesorů.

Odtud také pochází název **Vrstva abstrakce hardware (Hardware Abstraction Layer)**. Vyšším vrstvám poskytuje například rutiny pro komunikaci s periferními zařízeními. Kód HAL se nachází v souboru **hal.dll** v systémovém adresáři.

##### TVRDÉ JÁDRO

Nad HAL se nachází tenká vrstva, jež implementuje relativně jednoduché mechanismy, kterých využívají vyšší vrstvy jádra operačního systému pro stavbu složitějších struktur. Kód tvrdého jádra je pomocí vrstvy HAL odstíněn od většiny specifik hardware, a tudíž zde Assembleru najdete jen málo.

- **Mezi mechanismy implementované v této součásti patří:**
  - Algoritmus **plánování vláken** na procesoru.
  - Odložené volání procedur (**Deferred Procedure Call – DPC**).
  - Základní **synchronizační primitiva** jako událost (event), spinlock, semafor či pushlock.
  - Práce s hardwarovými přerušeními.
  - Část obsluhy systémových volání.

##### OVLADAČE

Ovladače umožňují správci vstupně/výstupních zařízení, který spolu s dalšími komponentami tvoří vrstvu označovanou jako **exekutiva**, komunikovat s různými typy hardware. Jedná se o spustitelné soubory formátu **PE** a jejich jméno většinou obsahuje koncovku **.sys**.

##### EXEKUTIVA

Exekutiva využívá tvrdého jádra k realizaci mnohem složitějších mechanismů, kterých mohou přes systémová volání nepřímo využívat obyčejné aplikace běžící v uživatelském režimu. Obsahuje ještě méně platformně specifického kódu než tvrdé jádro. Exekutiva se skládá z několika navzájem oddělených částí (viz obráze).

Ačkoliv se všechny nachází ve stejném adresovém prostoru, a tudíž by například správce objektů mohl přímo manipulovat s interními datovými strukturami, které náleží správci paměti, komunikují spolu pomocí ==přesně definovaných rozhraní==. Každá komponenta dává k dispozici sadu rutin, které může volat libovolný kód běžící v režimu jádra. Názvy některých funkcí a způsob realizace některých mechanismů připomínají techniky používané v objektově orientovaném programování.

![[9e2aa9d42dc408a203173254ffa7efc8c348b36d0fa0f236426088e9a24e938f.png]]

###### SPRÁVCE OBJEKTŮ (OBJECT MANAGER)

- **Správce objektů (Object Manager)** umožňuje vývojářům psát kód jádra podobně, jako by programovali v jazyce podporujícím konstrukty OOP.

Správce objektů například umožňuje jednotným způsobem objekty (otevřené soubory, klíče registru, paměťově mapované soubory) vytvářet a odstraňovat a obsahuje jednotný mechanismus řízení přístupu. Zjednodušeně lze říci, že správce objektů v sobě zapouzdřuje všechny principy, které platí pro většinu druhů objektů (při odstraňování objektu dochází k uvolnění paměti nezávisle na jeho typu, při vytváření nového objektu zase dochází k alokaci paměti, ať už se jedná o otevřený soubor, nebo klíč registru).

###### SPRÁVCE PAMĚTI (MEMORY MANAGER)

- **Správce paměti (Memory Manager)** se stará o všechny činnosti, které nějak souvisí s virtuální a fyzickou pamětí.

Přiděluje volné rámce fyzické paměti, zajišťuje správné mapování mezi virtuálními a fyzickými adresami a obsluhuje výpadky stránky. Vyřizování požadavků na přidělování a uvolňování bloků virtuální paměti o proměnlivé velikosti patří též do jeho kompetencí. Dále obsahuje bezpečnostní mechanismy jako **ASLR** (Address Space Layout Randomization).

###### SPRÁVCE PROCESŮ (PROCESS MANAGER)

- **Správce procesů (Process Manager)** má na starosti spouštění, běh a ukončení procesů a vláken.

Umožňuje ostatním součástím systému a běžným aplikacím zjistit informace o právě běžících procesech, měnit jejich prioritu, násilně je ukončovat a provádět další zajímavé akce.

###### SPRÁVCE VSTUPNĚ/VÝSTUPNÍCH ZAŘÍZENÍ (I/O MANAGER)

- **Správce vstupně/výstupních zařízení (I/O Manager)** zajišťuje většinu funkcí kolem ovladačů jádra a zařízení, ať už fyzických nebo virtuálních.

Díky této součástí může jádro za běhu načítat nové ovladače do svého paměťového prostoru a uvolňovat ty, které aktuálně nepotřebuje. Správce vstupně/výstupních zařízení též dovoluje ovladačům komunikovat mezi sebou. Komunikace probíhá přes objekty zvané zařízení (device), které si pro jednoduchost můžete představit jako kanály nebo roury mezi jednotlivými ovladači.

###### SPRÁVCE KONFIGURACÍ (CONFIGURATION MANAGER)

Windows patří mezi operační systémy, jejichž cílem je plnit co největší množství různorodých úkolů a přizpůsobit své chování co nejvíce požadavkům uživatele. Nastavení různých aspektů systému musí být někde uloženo a systém k němu musí mít snadný přístup. A způsob ukládání a práce s konfiguracemi je parketa pro součást exekutivy s názvem **správce konfigurací (Configuration Manager)**.

Na rozdíl od operačních systémů založených na Unixu, které většinu nastavení ukládají do textových souborů, Windows své konfigurace ukládá v ==binární podobě== – do tzv. **registru**. Registr funguje jako malá databáze, rychle se v něm vyhledává a manipuluje s jednotlivými položkami. Na rozdíl od textových souborů, dobře čitelných pro obyčejného člověka, pro prohlížení obsahu registru potřebujete speciální programy. Jedním z nich je **Editor registru (regedit.exe)**.

Vývojáři Windows se pro binární formu ukládání konfigurací rozhodli pravděpodobně z toho důvodu, že textové soubory se hůře a pomaleji počítačově zpracovávají a zabírají více místa. Logická struktura registru je téměř totožná s adresářovou strukturou na pevném disku. Adresáře se v této terminologii registru nazývají ==klíče== a souborům se říká ==hodnoty==.

Každý klíč může obsahovat libovolné množství dalších klíčů (podadresářů) a hodnot (souborů). Pouze hodnoty mohou obsahovat data.

**EDITOR REGISTRU**

![[af1aaecdb371b32182af05d3b8f6c5371a7b06009a33cbfdab67878bbcd3290b.png]]

###### BEZPEČNOSTNÍ MODEL

Operační systém také musí zajistit, aby každý mohl provádět jen operace, na které má dostatečná oprávnění. To je úkolem **bezpečnostního modelu (security model)**, který umožňuje pro každého uživatele nastavit, jaké činnosti smí a nesmí provádět. Díky bezpečnostnímu modelu může administrátor systému určit, k jakým objektům mají jednotliví uživatelé přístup.

Množina objektů přitom není omezena jenom na soubory a klíče registru; oprávnění lze nastavit i u procesů, vláken, nebo třeba synchronizačních primitiv. Bezpečnostní model Windows dále definuje sadu oprávnění, které uživatel potřebuje, aby mohl vykonávat určitou činnost. Do této kategorie patří například oprávnění vytvořit stránkovací soubor či povolení načíst ovladač do jádra.

##### SUBSYSTÉMY

Nad ntdll.dll se nachází vrstva knihoven, která tvoří součást prostředí pro obyčejné aplikace – tzv. **subsystému**. Rozhraní exportované touto vrstvou je již dobře dokumentováno, což znamená, že i v budoucích verzích Windows bude pravděpodobně fungovat stejně a maximálně jej Microsoft rozšíří. Vývojáři jej mohou používat ve svých aplikacích. Windows obsahuje **dva subsystémy** – ==Windows== a ==POSIX==.

Každý z nich dává programátorům aplikací k dispozici trochu odlišnou množinu funkcí obsažených v ntdll.dll. Například POSIX umožňuje vytvářet nové procesy pomocí rutiny **fork**, dobře známé z prostředí Unixu. Subsystém Windows takový způsob vytváření procesů neposkytuje. Nutnost implementovat POSIX také donutila vývojáře zavést do souborového systému NTFS **hardlinky**.

###### POSIX

- **POSIX** je zkratka z anglického sousloví portable operating system interface based on Unix (přenositelná systémová rozhraní založená na Unixu) a označuje sadu mezinárodních standardů, které popisují aplikační rozhraní v operačních systémech založených na Unixu.

Pokud by výrobci operačních systémů tyto standardy implementovali, rozhraní různých operačních systémů by byla definována stejně a stejně by se také chovala, což by ušetřilo práci programátorům aplikací, kteří by neměli tolik problémů s přenositelností na jiné platformy. Z historických důvodů Windows původně ze všech těchto standardů implementovaly pouze **POSIX 1**. Windows Vista a Windows Server 2008 s sebou přináší implementaci standardů POSIX v podobně **SUA** (Subsystem for Unix–based Application – subsystém pro aplikace založené na operačním systému Unix).

Tato rozšířená varianta subsystému POSIX implementuje kolem **2 000 funkcí** různých unixových aplikačních rozhraní a obsahuje kolem **tří set unixových programů**. Subsystém SUA je dostupný na Windows Server 2008 a v Ultimate a Enterprise edicích Windows Vista. Na rozdíl od subsystému Windows, bez kterého celý operační systém nemůže fungovat, ==POSIX se spouští jenom tehdy==, pokud si uživatel přeje spustit proces určený pro tento subsystém. Konfigurace obou subsystémů je uložena v registru pod klíčem

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Subsystems` jehož obsah vidíte na obrázku 2.6. Z obrázku je patrné, že hlavním procesem subsystému POSIX je **psxss.exe**, který se nachází v systémovém adresáři. Také vidíte, že hlavní proces subsystému Windows nese název **csrss.exe** a že subsystémy mají i komponentu běžící v režimu jádra. Jedná se o ovladač **win32k.sys**, který se stará o správu grafického uživatelského rozhraní a grafiky vůbec.

Na tomto místě může vyvstat otázka, proč každý subsystém nemá svůj vlastní ovladač jádra. Důvodem je vysoká duplicita kódu. Vývojáři Windows se rozhodli tomuto nebezpečí předejít, a proto subsystém POSIX využívá funkcí (a knihoven DLL) poskytovaných subsystémem Windows včetně ovladače win32k.sys. Situaci znázorňuje obrázek 2.7. Kdyby tomu tak nebylo, musely by existovat dvě sady knihoven DLL a dva různé ovladače pro obsluhu grafického uživatelského rozhraní.

Kód obou sad knihoven a ovladačů by však byl na mnoha místech totožný, což je v programování nežádoucí, protože dochází ke zvýšení rizika vzniku chyb.

###### WINDOWS

- Struktura subsystému Windows je složitější než v případě POSIXu. **Skládá se z následujících komponent:**
  - Hlavní proces subsystému **csrss.exe** a knihovny DLL, které používá.
  - Ovladač jádra **win32k.sys** a drivery grafické karty a videa.
  - Vrstva knihoven DLL zajišťující překlad volání dokumentovaných funkcí Windows API na volání nativních (a často nedokumentovaných) rutin z knihovny **ntdll.dll**, která je zodpovědná za volání jádra. Mezi tyto knihovny patří kernel32.dll, user32.dll, gid32.dll či advapi32.dll.

Mezi úkoly hlavního procesu subsystému patří vykreslování oken konzolových aplikací a podpora 16bitových programů určených původně pro operační systém MS–DOS. Csrss.exe také dostane oznámení, kdykoliv dojde k spuštění nového či ukončení již běžícího procesu nebo vlákna. Ve svém adresovém prostoru si uchovává vlastní kopii seznamu všech běžících procesů a vláken, aby pro ně mohl vyřizovat požadavky, jež mohou vzniknout při volání některých funkcí Windows API. V dobách předcházejících Windows NT 4 do hlavního procesu subsystému patřily i moduly, které se starají o grafické uživatelské rozhraní a grafické kreslení vůbec.

Vývojáři se tímto uspořádáním pravděpodobně chtěli přiblížit elegantní struktuře operačních systémů založených na mikrojádru. Taková struktura však vyžadovala velmi častá systémová volání a přepínání kontextu procesů. Ovladače grafické karty a obrazovky totiž běžely v režimu jádra, takže pokud nějaká aplikace chtěla například překreslit okno, bylo nutné přepnout kontext na hlavní proces subsystému, kde sídlil správce grafického uživatelského rozhraní, a následně se přepnout do režimu jádra, aby ten mohl doručit požadavek na překreslení ovladači grafické karty.

Systémová volání a přepínání kontextu mezi procesy patří mezi časově náročné operace, což mělo negativní dopad na výkon systému jako celku. Situace se výrazně nezlepšila ani po provedení mnoha optimalizací (byl upraven plánovač procesů a csrss.exe dokonce mohl číst některé oblasti paměti jádra, aby se ušetřilo kopírování). Vývojáři proto ve Windows NT 4 přesunuli správce grafického uživatelského rozhraní a ostatní grafické funkce do ovladače **win32k.sys**, čímž se snížil počet systémových volání a přepínání procesů.

Jak již víte, jádro systému sdílí společný paměťový prostor a může komunikovat s ovladači grafické karty bez použití systémových volání. Ovladač win32k.sys se tedy stará o grafické uživatelské rozhraní; spravuje okna, tlačítka, textová pole, obsluhuje myš a klávesnici. Umožňuje také kreslení různých grafických útvarů, jako jsou body, přímky či křivky.

Ovladač se postará, aby se požadavky na vykreslování dostaly k správným ovladačům grafiky, tudíž aplikace, jež využívají GUI, vůbec nemusí (a většinou ani nepotřebují) vědět, jakou grafickou kartou počítač disponuje a jak se s ní zachází. Win32k.sys se chová podobně jako **HAL** – smazává rozdíly mezi různými kusy hardware. Bránu k ovladači win32k.sys tvoří knihovny **gdi32.dll** a **user32.dll**. První z nich obsahuje rutiny pro kreslení různých grafických útvarů (body, čáry, křivky) a druhá exportuje funkce pro práci s prvky uživatelského rozhraní, jako jsou okna, menu či ikony.

Mezi velmi důležité knihovny DLL také patří **kernel32.dll**, jenž exportuje vybrané části exekutivy (práce s procesy a vlákny, správa paměti, synchronizace), a **advapi32.dll**, která obsahuje rozhraní pro práci se službami a bezpečnostním modelem.

###### REGISTR

![[2a7a088d496e4285ab6c9599c9bf160424fe8f8ff33abfd4aa11d98c92abe4b2.png]]

###### ZÁVISLOST SUBSYSTÉMU POSIX NA SUBSYSTÉMU WINDOWS

![[c11b1667ac0d818a31e5bfa6372be9fdfb5f043b53b8e35baab1965861a41c8c.png]]

**PRO HACKERY**

> [!warning] Pro hackery
> - Správce úloh vám nedovolí systémové procesy násilně ukončit. Pokud se o to pokusíte, program zareaguje hláškou „Přístup odepřen“.
> - Zajímavá je zde metoda, jakou Správce úloh rozhoduje, zda cílový proces je systémový.
> - Až do Windows Vista totiž nejsou tyto procesy chráněny žádným bezpečnostním mechanismem, který by bránil jinému procesu, jenž disponuje administrátorským oprávněním, je ukončit.
> - Správce úloh má v sobě „natvrdo“ zakódovány názvy procesů, které považuje za systémové.
> - Tohoto faktu mohou snadno zneužít tvůrci malware.
> - Zkuste si například pojmenovat nějaký program winlogon.exe, spustit jej a následně se jej pokuste násilně ukončit pomocí Správce úloh.

##### SYSTÉMOVÉ PROCESY

Windows patří mezi **monolitické** operační systémy, které se vyznačují velmi velkým a složitým jádrem, jež disponuje řadou pokročilých funkcí. Přesto běh systému závisí na několika procesech, jejichž ukončení (ať je způsobeno úmyslně, nebo v důsledku softwarové chyby) znamená ==restartování počítače==. Tyto kritické procesy se obvykle nazývají jako **systémové**.

Seznam právě běžících procesů můžete vidět v programu Správce úloh, který spustíte například pomocí známé klávesové zkratky **Ctrl+Alt+Del**.

![[5b8c434a0c98691cdd501acd37e872fb463bc7fc902d8806f0388a7862242934.png]]

###### PRO HACKERY

> [!warning] Pro hackery
> - Správce úloh vám nedovolí systémové procesy násilně ukončit. Pokud se o to pokusíte, program zareaguje hláškou „Přístup odepřen“.
> - Zajímavá je zde metoda, jakou Správce úloh rozhoduje, zda cílový proces je systémový.
> - Až do Windows Vista totiž nejsou tyto procesy chráněny žádným bezpečnostním mechanismem, který by bránil jinému procesu, jenž disponuje administrátorským oprávněním, je ukončit.
> - Správce úloh má v sobě „natvrdo“ zakódovány názvy procesů, které považuje za systémové.
> - Tohoto faktu mohou snadno zneužít tvůrci malware.
> - Zkuste si například pojmenovat nějaký program winlogon.exe, spustit jej a následně se jej pokuste násilně ukončit pomocí Správce úloh.

###### NEČINNÉ PROCESY (SYSTEM IDLE PROCESSES

- **Nečinné procesy (System Idle Processes)**

Jedná se pouze o **pseudoproces**, který nevykonává žádnou činnost v uživatelském režimu. Na disku nenajdete žádný soubor, který by obsahoval jeho kód a data, ani žádné knihovny DLL, jenž by využíval. Úkolem Nečinných procesů je spotřebovávat čas procesoru, když žádná součást operačního systému ani žádná aplikace nemá co na práci.

Jádro vytvoří tento proces během raných fází inicializace operačního systému.

- ==PID== Nečinných procesů je vždy roven ==nule==.

###### PROCES SYSTEM

- **Proces System**

Proces System také nevykonává žádný kód v uživatelském režimu, a tudíž nepoužívá žádné knihovny DLL a nenajdete žádný soubor s příponou .exe, který by jej reprezentoval. Už ale nejde čistě o pseudoproces; v jeho kontextu běží skupina vláken známá pod označením **pracovní vlákna (worker threads)**. Jádro tato vlákna vytvoří během bootovacího procesu a jejich úkolem je vykonávat činnosti, jenž jim někdo zadá.

Pracovní vlákna stráví většinu času čekáním, až jim nějaká součást jádra (nebo ovladač) určí, co mají vykonat. Jakmile práci dokončí, čekají na další zadání. Jádro využije služeb pracovních vláken ve chvíli, kdy potřebuje vykonat úkol, který je časově náročný (a tudíž by mohl brzdit výkon systému, kdyby nebyl proveden asynchronně), nebo nemůže být splněn za aktuálních podmínek. V takovém případě jádro předá úkol na bedra této speciální skupině vláken.

Vlákna většinou dokončují zpracování požadavků od hardware, které nebylo možné provést při obsluze přerušení. Dále je využívá například správce paměti pro zapisování „špinavých“ (dirty) stránek z vyrovnávací paměti na disk. Spolu s Nečinnými procesy je System jediným procesem s pevně daným číslem **PID**.

Toto číslo má v jeho případě od Windows 2000 hodnotu ==4==. V předcházejících verzích neslo hodnotu ==1==.

###### SPRÁVCE RELACÍ (SESSION MANAGER)

- **Správce relací (Session Manager, Smss.exe)**

Smss.exe je spuštěn v poslední fázi startu jádra a jedná se o ==první proces==, který vykonává kód v uživatelském režimu. Provede poslední fázi inicializace operačního systému, který je pak připraven na přihlášení uživatelů. Jak název napovídá, hlavním úkolem tohoto procesu je vytváření **relací**.

Relaci si můžete představit jako ohradu, ze které ten, kdo je v ní uzavřen, nevidí ven a zároveň nikdo nevidí dovnitř. Tyto ohrady se využívají pro oddělení prostoru jednotlivých uživatelů. Díky nim například každý uživatel může mít namapované disky pod jinými písmeny.

- Jednotlivé relace se označují číslem.

Smss.exe nejprve vytvoří **relaci 0**, která se též označuje jako **konzolová relace**. V rámci ní běží systémové procesy, služby a všechny procesy uživatele, který se přihlásí jako první. Pro každého dalšího uživatele vytvoří správce další relaci. Pro každou novou relaci správce spustí jednu kopii procesu **winlogon.exe**.

Smss.exe je též zodpovědný za inicializaci hlavního procesu subsystému Windows – **csrss.exe**. Pro relaci 0 se místo Winlogonu spouští **wininit.exe**. Jakmile dokončí svoji práci, správce relací navždy hlídá hlavní proces subsystému Windows a všechny kopie programu winlogon.exe. Pokud zjistí, že některý z těchto procesů byl neočekávaně ukončen, vyvolá modrou obrazovku smrti s kódem `STATUS_CRITICAL_SYSTEM_ PROCESS_DIED`

###### PROCESY PODÍLEJÍCÍ SE NA PŘIHLÁŠENÍ UŽIVATELE (WINLOGON.EXE, LSASS.EXE)

- **Procesy podílející se na přihlašování uživatele (winlogon.exe, LSASS.exe)**

Úkolem procesu **winlogon.exe** je umožnit uživateli přihlášení pomocí grafického uživatelského rozhraní. Může autentizovat uživatele různými způsoby, nejčastěji se ale stále používá zadání uživatelského jména (login) a hesla. Jednotlivé metody autentizace jsou implementovány v oddělených knihovnách DLL. Winlogon v sobě má zabudovanou jednoduchou metodu ==ochrany proti programům==, které se snaží zachytit údaje, jež uživatel zadal při pokusu o přihlášení.

Většinou se jedná o tzv. **keyloggery** – programy, které zaznamenávají stisky jednotlivých kláves. Aby takový program nemohl přesně určit, kdy uživatel zadává přihlašovací údaje, může být Winlogon nastaven takovým způsobem, že před zobrazením přihlašovací obrazovky (viz obrázek) je třeba stisknout speciální kombinaci kláves. Obrazovku, která uživatele vyzývá k stisku této kombinace kláves, vidíte na obrázku; její podoba se může mírně lišit v závislosti na verzi operačního systému.

Jako výchozí kombinace je nastaven známý „trojhmat“ **Ctrl+Alt+Del**. Trik spočívá v tom, že jakmile Winlogon zjistí, že tato kombinace byla stisknuta, tuto informaci pohltí a zobrazí okno, kam uživatel vyplní přihlašovací údaje. Přesněji, o stisku aktivační kombinace se dozví okno s názvem **SAS Window**, které je též zodpovědné za její pohlcení.

Pokud tedy keylogger neoperuje v samotném jádře systému nebo neinfiltroval do adresového prostoru procesu winlogon.exe (například v podobě knihovny DLL), nemůže stisk aktivační kombinace přímo detekovat, a tedy přesně zjistit, kdy uživatel zadává přihlašovací údaje. Jakmile uživatel zadá login a heslo, Winlogon tyto údaje odešle procesu **lsass.exe**, kde proběhne jejich ověření. Pokud vše dopadne dobře (uživatel zadal správné jméno a heslo), lsass.exe zjistí, jakými oprávněními uživatel disponuje, a vytvoří tzv. **token**. Jedná se o objekt, kterým se pak uživatel prokazuje, potřebuje-li doložit, že má oprávnění k provedení určité operace.

- Pokud má uživatel administrátorská práva a je-li zapnut mechanismus **UAC** (User Account Control), lsass.exe vytvoří ==tokeny dva==.
  - První z nich v sobě obsahuje všechna oprávnění, kterými uživatel disponuje.
  - Druhý obsahuje jenom vybraná z nich.
  - S pomocí druhého tokenu pak Winlogon vytvoří procesy, které provedou inicializaci prostředí.
  - Token s omezenými právy se použije, kdykoliv uživatel spustí nějakou aplikaci, jež nevyžaduje administrátorská práva.

Pokud se uživatel pokusí spustit program vyžadující oprávnění administrátora, UAC se může dotázat (záleží na nastavení systému), zda chce daný program, který vyžaduje administrátorská práva, a tudíž by mohl být pro systém nebezpečný, spustit. Pokud dá uživatel spuštění zelenou, použije se pro daný program token, který obsahuje všechna uživatelova oprávnění. Winlogon zůstává aktivní i po úspěšném přihlášení uživatele.

Kromě toho, že je jeho povinností zajistit i odhlášení, stále čeká na onu aktivační klávesovou kombinaci a v případě, že zjistí její stisknutí, zobrazí dialog, který vidíte na obrázku. Winlogon také může být nakonfigurován tak, že spustí rovnou Správce úloh. Jakmile Winlogon obdrží tokeny od LSASS, může být zahájena inicializace pracovního prostředí uživatele. Tato činnost již nespadá do pravomocí tohoto procesu, ale do kompetence procesů, jejichž názvy jsou uvedeny v hodnotě **Userinit** v klíči

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\Current Version\Winlogon`. Winlogon přečte obsah této hodnoty a pokusí se všechny nalezené procesy spustit. Inicializace pracovního prostředí spočívá v podstatě jen ve spuštění startovacích skriptů a předání řízení shellu, jehož název **userinit.exe** nalezne pod hodnotou **Shell** ve stejném klíči, jako Winlogon hledal hodnotu Userinit.

Výchozím shellem pro všechny uživatele je **Průzkumník Windows (explorer.exe)**, který zodpovídá za zobrazení pracovní plochy a umožňuje uživateli mimo jiné procházet adresářovou strukturu a spouštět další programy.

**PŘIHLAŠOVACÍ OBRAZOVKA**

![[4eb84a308f44c47665b1119b0fa6d9375998fff79aeb0269500a19e31c80e78f.png]]

**VÝZVA KE STISKU AKTIVAČNÍ KOMBINACE KLÁVES**

![[2e1563bf79f72e28af6101c4c249e7cb7a6fdf4efe8634289d2adbeb7b18982b.png]]

**DIALOG WINLOGON**

![[6b7fa5477c79daf85ca99990fb51da73f92a81756e818fab611f9e75495e6e35.png]]

**PRO HACKERY**

> [!warning] Pro hackery
> - Jediný proces, který by se měl za všech okolností starat o inicializaci pracovního prostředí uživatele, je userinit.exe v systémovém adresáři.
> - Pokud hodnota obsahuje i názvy dalších procesů, jedná se pravděpodobně o malware.

###### PROCESY PRO PODBORU SLUŽEB (SERVICES.EXE., SVCHOST.EXE)

- **Procesy pro podporu služeb (services.exe, svchost.exe)**

Mnoho součástí Windows je implementováno jako **služby** – programy běžící na pozadí, které ve většině případů nepotřebují (a ani nevyhledávají) interakci s uživatelem a jejichž běh nezávisí na tom, zda je přihlášen či nikoliv. Interně systém Windows mezi služby řadí i ovladače jádra, ačkoliv ty nepatří mezi entity, o které se správce služeb (Service Control Manager – SCM), reprezentovaný procesem services.exe, příliš stará. Jeho hlavním úkolem je instalovat, spouštět a zastavovat služby určené pro běh v uživatelském režimu a posílat jim další druhy příkazů.

Službu tvoří obyčejný spustitelný soubor formátu **PE** s příponou .exe, který navíc obsahuje speciální kód pro komunikaci se správcem. Na rozdíl od normálních aplikací, více služeb může sdílet virtuální adresový prostor jednoho procesu. Vše záleží na nastavení konkrétní entity. Kód služeb, které nemají vlastní proces, je vykonáván v kontextu instancí procesu **svchost.exe**, který je pro jejich „hostování“ přímo určen.

Pro pohodlnou kontrolu služeb je připravena aplikace **services.msc**, která nejen zobrazí seznam všech nainstalovaných služeb a jejich aktuální stav, ale umožňuji s nimi i manipulovat. Uživatelské rozhraní tohoto programu vidíte na obrázku. Konfigurace všech služeb se nachází v registru pod klíčem `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services`.

**SLUŽBY**

![[c32c8077b73ebb39e9aa65ef86428af4063793647be2aa29e64c35e442aa2a34.png]]

**NASTAVEN´SLUŽBY TCPIP V REGISTRU**

Hodnoty **Description** a **DisplayName** mají pouze informativní charakter. Jejich obsah zobrazuje snap-in services.msc ve sloupcích Název a Popis. Pokud je hodnota DisplayName prázdná, nebo vůbec neexistuje, utilita zobrazí ve sloupci Název interní jméno. Položka **ErrorControl** určuje, jak se má správce zachovat, když při spouštění služby dojde k chybě. Možné hodnoty a popis chování správce naleznete v tabulce Hodnota **ImagePath** v sobě uchovává název souboru služby. Pokud není hodnota přítomna, SCM předpokládá, že soubor služby se nachází v systémovém adresáři a jmenuje se X.exe, nebo X.sys, kde X je interní název služby.

Podle hodnoty **Start** se SCM rozhodne, kdy může být služba spuštěna. Položka **Type** určuje, zda se jedná o službu běžící v uživatelském režimu, nebo o ovladač jádra. Možné hodnoty vidíte v tabulce. Způsob a čas spuštění služby lze tedy ovlivnit hodnotou položky Start v jejím registrovém klíči.

Toto nastavení lze zjemnit přiřazením služby do určité **skupiny**. Výčet všech dostupných skupin včetně pořadí, v jakém budou procházeny při spouštění jednotlivých služeb, se nachází v klíči `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\ServiceGroupOrder`. Pro ovladače je možné určit i pořadí spouštění jednotlivých entit ve skupině. Slouží k tomu hodnota **Tag**. Pořadí spouštění jednotlivých entit v jedné skupině na základě jejich tagu je uloženo v klíči

`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GroupOrderList` Některé služby mohou svoji činnost vykonávat pouze za předpokladu, že běží služby jiné. Například služba Zvuk systému Windows je závislá na službách Koncové vytváření služby Windows Audio, Vzdálené volání procedur a Služba Plánovač multimédií. Pokud nějaká z nich není aktivní, nelze spustit ani Zvuk Systému Windows.

Služby mohou být závislé nejen na jiných službách, ale i na celých skupinách. Systém může spustit službu závislou na skupině, pokud je alespoň jedna entita z této skupiny aktivní.

![[e361a865ed678a5f0ca967900c5c712b551514c20f55a79028e4a2cbbaea60a8.png]]

**ERROR**

![[63d4edcb9c60fafe2eb818e43a8ec401d1c3c7bba994982fd995be14585f9979.png]]

**START**

![[8d610b25c4cbec28d83cb04e2a297b5dbff4fab7c17418ab4942336105e3f937.png]]

**TYPE**

![[793d867f7298f742d244b243aec1f4dac96c1215af3ee3714dfc844c0490959b.png]]

#### SERVEROVÉ EDICE

Serverové edice používají totéž jádro jako desktopové edice a jsou k dispozici další nástroje (**DHCP server, DNS Server, Active Directory**, ...).

![[6ec1a6fb8def4315e0d84f3de39c75061b414bed4ab5b82fa28a5114fd34da0e.png]]

---

**Struktura OS:** [[01_STRUKTURA_OPERAČNÍCH_SYSTÉMŮ (1)|Architektury OS]] · [[01a_Windows|Windows]] · [[01b_Unix|UNIX]] · [[01c_Linux|Linux]] · [[01d_Apple|Apple]] · [[01e_Android|Android]]
