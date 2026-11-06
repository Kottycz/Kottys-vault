---
aliases: [Struktura operačních systémů, Struktura OS, Architektura OS, Architektury jader]
tags: [os]
---

# ARCHITEKTURA OS

> Přepis xmind mapy **01_STRUKTURA_OPERAČNÍCH_SYSTÉMŮ** (Teams) – stejná struktura a texty jako v mapě, jen přehledněji rozdělené do odrážek a se zvýrazněnými pojmy. Obrázky se zobrazí, když složku `resources` z xmindu zkopíruješ do vaultu.

## STRUKTURA OS

Abychom mohli porozumět tomu, jak pracují operační systémy, uveďme si alespoň základní informace o jejich **struktuře** a s tím související pojmy. U moderních OS je struktura vytvářena především s ohledem na ==bezpečnost a stabilitu== celého systému.

### Hardwarová ochrana prostředků

Moderní operační systémy využívají **hardwarovou ochranu prostředků**. Na procesorech řady x86 je tato ochrana implementována ve formě ==čtyř okruhů (RING 0 až RING 3)==. Každý proces běží v režimu některého z těchto okruhů a to určuje jeho možnosti v přístupu k chráněným prostředkům (přímý přístup k hardware = paměť, I/O, procesor = využívání některých strojových instrukcí).

Většina OS používá pouze **2 okruhy**: **RING 0** pro jádro systému a **RING 3** pro ostatní procesy.

- **RING1 a RING2** lze využít pro další škálování přístupových oprávnění a můžeme se s tím setkat u některých virtualizačních technik, zejména na serverech.

![[Pasted image 20261001123504.png]]


### Režimy běhu procesů

Abychom mohli porozumět tomu, jak pracují operační systémy, uveďme si alespoň základní informace o jejich struktuře a s tím související pojmy. U moderních OS je struktura vytvářena především s ohledem na bezpečnost a stabilitu celého systému. Vždy najdeme rozdělení běhu procesů na **privilegovaný režim** (režim jádra, kernel mode) a **neprivilegovaný režim** (uživatelský režim, user mode).

V privilegovaném režimu běži procesy **jádra** operačního systému a v uživatelském režimu běží **aplikace**. Procesy běžící v uživatelském režimu nemají možnost jakkoliv zasahovat do privilegované části.

![[Pasted image 20261001123532.png|245]]

- **Privilegovaný režim** = Režim jádra
- **Uživatelský režim** = Režim aplikací

**Poznámka z hodiny (OPS)**

> [!abstract] Operační systém
> Co potřebujeme:
>
> - ==správce CPU== – `ring 0`
> - ==správce paměti== – `ring 0`
> - ==správce I/O== – `ring 0`
> - ==grafické rozhraní== **GUI** nebo **CLI** – stačí `ring 3`
> - ==souborový systém==

> [!tip] Ring 0 a Ring 3
> - Programy v `ring 0` říkáme ==kernel==
> - **Ring 0** = ==jádro==
> - **Ring 3** = ==aplikace==

### A jak to spolu souvisí

Většina OS používá pouze 2 okruhy, **RING 0** pro jádro systému a **RING 3** pro ostatní procesy. RING1 a RING2 lze využít pro další škálování přístupových oprávnění a můžeme se s tím setkat u některých virtualizačních technik, zejména na serverech.

- **Procesor** je hlavním nástrojem operačního systému, který tento malý čip využívá k různým vlastním výpočtům a dává jej k dispozici i aplikacím, jež vy jako uživatel spouštíte.

Procesor v sobě implementuje řadu mechanismů, kterých operační systém využívá například pro zaručení ochrany hardwaru před zneužitím zákeřným programem či pro ochranu kódu svého jádra před nežádoucími modifikacemi. Mezi tyto mechanismy patří možnost vykonávat kód programu na **několika úrovních oprávnění**, přičemž každá z nich přesně definuje, které operace jsou povoleny a které zakázány. Omezení se vztahuje například na druhy instrukcí, jež lze na jednotlivých úrovních použít.

Například procesory Intel kompatibilní s architekturou x86 mají v sobě zabudovány čtyři různé úrovně oprávnění. Tyto úrovně se často označují jako **ring módy (rings)** a obvykle se číslují od 0 do 3. ==Čím nižší číslo, tím větší volnost== má kód běžící na dané úrovni.

Program vykonávaný na úrovni **Ring 0** má dovoleno využít veškeré možnosti, které mu instrukční sada procesoru nabízí – může přímo komunikovat s hardware, ovládat chování procesoru či měnit obsah důležitých systémových datových struktur, jako je tabulka vektorů přerušení či globální tabulka segmentů. Úrovně **Ring 1 a Ring 2** již některé instrukce vykonávat nepovolují a kódu běžícímu na úrovni **Ring 3** procesor neumožňuje žádným způsobem přímo měnit nastavení, která by mohla ovlivnit chování operačního systému. Úroveň Ring 3 například nedovoluje přímou komunikaci s hardware.

Z historických důvodů **Windows používají pouze úrovně Ring 0**, na které běží veškerý kód jádra a ovladačů, **a Ring 3**, která slouží pro vykonávání kódu normálních aplikací (též označovaných jako procesy). Obecně se úroveň, která poskytuje nejvyšší možná oprávnění, označuje jako **režim jádra (kernel mode)**. Naopak úroveň kladoucí nejvyšší omezení na vykonávaný kód se nazývá **uživatelský režim (user mode)**.

![[Pasted image 20261001123708.png]]



### VYUŽITÍ RING 1 PŘI VIRTUALIZACI

RING1 a RING2 lze využít pro další škálování přístupových oprávnění a můžeme se s tím setkat u některých virtualizačních technik, zejména na serverech. Implementace virtualizace spočívá v tom, že na HW počítače se nainstaluje vrstva software ==HYPERVISOR== a teprve nad tento HYPERVISOR se instalují operační systémy.

- **Hypervisor** představuje rozhraní mezi HW a hostovanými operačními systémy.

Ve směru k HW zajišťuje jeho management a optimální vytěžování (load ballancing). Operačním systémům poskytuje abstrakci HW a iluzi, že OS běží na určité HW konfiguraci dle nastavení virtuálního počítače izolovaně od ostatních OS.

![[Pasted image 20261001123623.png]]

#### PRINCIP VIRTUALIZACE

![[Pasted image 20261001123739.png]]

### ZÁKLADNÍ TYPY ARCHITEKTUR

Následující typy struktur jsou obecně používány pro výpočetní systémy jako celek i pro jejich jednotlivé součásti (strukturu jádra, vrstev v jádře, ovladačů I/O, služeb OS, funkcí OS).

![[Pasted image 20261001123754.png]]

#### MONOLITICKÁ

Monolitická struktura je **nejjednodušší** struktura používaná v jádrech operačních systémů nebo v zařízeních. Systém se skládá z **jádra** a **rozhraní**, které zprostředkovává komunikaci mezi jádrem a okolím. Samotné jádro je představováno obvykle **jedním souborem** (při startu systému se jádro načítá z jediného souboru). Například u Linuxu je to soubor s názvem `/boot/vmlinuz`.

Funkcionalita je rozšiřována za běhu připojovanými **moduly** (knihovnami, např. DLL ve Windows). Jádra **UNIXOVÝCH** a **WINDOWS S NT** systémů jsou monolitická jádra (i když mají přesně rozvrženou vnitřní strukturu).



##### MS DOS

![[Pasted image 20261001124053.png]]

##### TRADIČNÍ UNIX

![[Pasted image 20261001124146.png]]

#### MICROKERNEL

Jak již název napovídá, systémy založené na mikrojádru (**mikrokernel**), obsahují velmi **malé jádro**, které implementuje pouze některé základní mechanismy jako **virtuální paměť, plánování vláken, obsluhu výjimek a komunikaci mezi procesy**. Ostatní komponenty (souborové systémy, síťová komunikace, správce procesů, správce paměti, I/O) běží v **uživatelském režimu** jako aplikace. Mezi **výhody** architektury založené na mikrojádru patří ==vyšší stabilita== a menší nároky na programátorské schopnosti vývojářů systému.

Protože většina součástí běží v uživatelském režimu, selhání jedné z nich nemusí znamenat pád celého systému – například není možné narušit integritu jádra nechtěným přepsáním jeho datových struktur v ovladači souborového systému. Při případné chybě v součásti systému často stačí příslušnou komponentu restartovat a systém může pokračovat ve své činnosti. Malé jádro tedy znamená méně kritického kódu (kódu, který může způsobit selhání celého systému)

![[fba5ffd0d5c60f803acd8e23d938bd2bf80316df154a54c4cecd7c175f9a31b2.png]]

##### MACH

![[8e1bf37924d04cb1b6a6c1dc6dd37914895c040c5bdc60848bcd6ad84cacf8df.jpg]]

##### HURD

![[2376707942dad8c18d26f0f01b09dfb853a353c58f4e34e3a99afeee2a3871a2.png]]

- https://www.gnu.org/software/hurd/

##### OS X

![[6df8bc3fc3c2887ebd6feedff10dc94ac4f39e96f591ae68bd0f07b870b3dc95.gif]]

###### OS X DETAILNĚJI

![[61ba59654d93358a6531fe3b580abbfb28b277790157378d29b77d9c88758e44.svg]]

#### VRSTVENÁ/HIERARCHICKÁ

- Části systému jsou uspořádány do **vrstev**.

Každá vrstva využívá služeb **nižších** vrstev, ne naopak. Každá vrstva komunikuje právě jen s okolními vrstvami. Systém je budován od vnitřních vrstev k vnějším, proto vnitřní vrstvy, které jsou nejdůležitější z hlediska výkonu, stability a bezpečnosti, bývají nejlépe otestovány.

V IT se s touto architekturou setkáváme například u počítačových sítí (model ISO/OSI, TCP/IP). V oblasti operačních systémů je takto obvykle reprezentován OS jako celek. Rozlišujeme především dvě hlavní vrstvy: ==VRSTVU JÁDRA== a ==UŽIVATELSKOU VRSTVU==.

![[336722f12d976223721595688249346fd0f2af494c432b115dcdd4d1e5495403.png]]

#### MODULÁRNÍ

Jádro poskytuje **základní služby** jako plánování a řízení procesů, paměti, obsluhu vyjímek, přerušení a ostatní služby jsou do jádra nahrávány ==dynamicky== při startu nebo při běhu systému (v okamžiku, kdy jsou poprvé použity). Tak je do jádra dynamicky nahrána například podpora různých souborových systémů, ovladače, síťové protokoly, bez nutnosti překompilovat jádro. Tento přístup předpokládá precizně definované a unifikované rozhraní modulů, přes které může jádro komunikovat i s takovým modulem, který v době vzniku jádra ještě neexistoval.

Výhoda oproti MIKROKERNEL architektury je v tom, že tím, že se moduly stanou **součástí jádra**, mohou spolu komunikovat přímo, aniž by si museli posílat zprávy prostřednictvím jádra. Tato architektura je stále více využívána v moderních OS jako **SOLARIS, LINUX, MAC OS X, WINDOWS**.

![[96f61bd631f92fe473edb29c022d26110cb020b283705683042f4dedcc8c79ab.png]]

#### HYBRIDNÍ

V praxi je jen velmi málo operačních systémů založeno na jedné, striktně definované struktuře. Velmi často **kombinují více přístupů**, aby dosáhli co nejlepší kombinace výkonu, bezpečnosti a použitelnosti.

- **LINUX** i **Solaris** jsou monolitické systémy, protože systém běží v jediném adresovém prostoru a poskytuje tak vysoký výkon. Jsou také modulární a nová funkcionalita je do jádra připojována dynamicky.
- **Windows** jsou také hlavně monolitický systém (primárně z důvodu výkonnosti) ale zůstává v nich i chování typické pro mikrokernel systém včetně podpory různých subsystémů, které běží v uživatelském režimu a současně Windows podporují také dynamicky připojované moduly jádra.

![[434b903d4fae000fff60782340b6ae74476742f793cd8725985c423b068559ae.png]]

##### WINDOWS S NT JÁDREM

![[3f54fb54a230b50c1ee0b6af61be5ce8119b2bd950701c9e440d138494f8a9c6.png]]

##### GNU/LINUX

![[a60c2df2756acd3c915c9b76efcb81261fdcb21224856c6cb650f051a0689565.png]]

#### POROVNÁNÍ MONOLITIC-MICROKERNEL-HYBRID

![[2dd4f64029e8f74bf190689014312e626596b3eebcf64e8806fd67a60d14e9f4.png]]

## ZDROJE

- http://www.vmware.com/download/player/
- https://www.osboxes.org/vmware-images/
- http://www.vmware.com/appliances/

---

**Struktura OS:** [[01_STRUKTURA_OPERAČNÍCH_SYSTÉMŮ (1)|Architektury OS]] · [[01a_Windows|Windows]] · [[01b_Unix|UNIX]] · [[01c_Linux|Linux]] · [[01d_Apple|Apple]] · [[01e_Android|Android]]
